---
title: "Using Cert Manager"
date: 2020-12-13T00:03:10-08:00
draft: false
---

# Concept

- Issuer: Issuers, and ClusterIssuers, are Kubernetes resources that represent certificate authorities (CAs) that are able to generate signed certificates by honoring certificate signing requests. All cert-manager certificates require a referenced issuer that is in a ready condition to attempt to honor the request.
- Certificate: cert-manager has the concept of Certificates that define a desired x509 certificate which will be renewed and kept up to date. A Certificate is a namespaced resource that references an Issuer or ClusterIssuer that determine what will be honoring the certificate request.

# Installtion

```bash
# Kubernetes 1.16+
$ kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.0.4/cert-manager.yaml
```

# Configurations

## Configure a self-signed issuer

The SelfSigned issuer doesn’t represent a certificate authority as such, but instead denotes that certificates will be signed through “self signing” using the given private key. This means that the provided private key of the resulting certificate will be used to sign its own certificate.

```yaml
apiVersion: cert-manager.io/v1
kind: Issuer
metadata:
  name: selfsigned-issuer
  namespace: sandbox
spec:
  selfSigned: {}
```

## Configure an ACME (Let's Encrypt) issuer

The ACME Issuer type represents a single account registered with the Automated Certificate Management Environment (ACME) Certificate Authority server. When you create a new ACME Issuer, cert-manager will generate a private key which is used to identify you with the ACME server.

```yaml
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata:
  name: letsencrypt-staging
spec:
  acme:
    # You must replace this email address with your own.
    # Let's Encrypt will use this to contact you about expiring
    # certificates, and issues related to your account.
    email: user@example.com
    server: https://acme-staging-v02.api.letsencrypt.org/directory
    privateKeySecretRef:
      # Secret resource that will be used to store the account's private key.
      name: example-issuer-account-key
    # Add a single challenge solver, HTTP01 using nginx
    solvers:
    - http01:
        ingress:
          class: nginx
```

# Usage

## Secure the Ingress resource

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    # add an annotation indicating the issuer to use.
    cert-manager.io/cluster-issuer: nameOfClusterIssuer
  name: myIngress
  namespace: myIngress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - backend:
          serviceName: myservice
          servicePort: 80
        path: /
  tls: # < placing a host in the TLS config will indicate a certificate should be created
  - hosts:
    - example.com
    secretName: myingress-cert # < cert-manager will store the created certificate in this secret.
```

## Secure the ISTIO gateway

Create a certificate resource under the same namespace as `istio-ingressgateway` 

```yaml
apiVersion: cert-manager.io/v1alpha2
kind: Certificate
metadata:
  name: ingress-cert
  namespace: istio-system
spec:
  secretName: ingress-cert
  commonName: my.example.com
  dnsNames:
  - my.example.com
  ...
```
Refer to the certificate in the TLS section
```yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: gateway
spec:
  selector:
    istio: ingressgateway
  servers:
  - port:
      number: 443
      name: https
      protocol: HTTPS
    tls:
      mode: SIMPLE
      credentialName: ingress-cert # This should match the Certificate secretName
    hosts:
    - my.example.com # This should match a DNS name in the Certificate
```
# Setup DNS challenge using Route53 (to setup ClusterIssuer with Let's encrypt)

Create an IAM policy

```yaml
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "route53:GetChange",
            "Resource": "arn:aws:route53:::change/*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "route53:ChangeResourceRecordSets",
                "route53:ListResourceRecordSets"
            ],
            "Resource": "arn:aws:route53:::hostedzone/*"
        },
        {
            "Sid": "VisualEditor2",
            "Effect": "Allow",
            "Action": "route53:ListHostedZonesByName",
            "Resource": "*"
        }
    ]
}
```
