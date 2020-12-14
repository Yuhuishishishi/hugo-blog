---
title: "Setup Hugo Blog"
date: 2020-12-12T00:44:54-08:00
draft: false
---

I recently encountered the idea of static site generator, and started to learn using Hugo. I find it extremely convenient especially 
when using with PaaS deployment tools such as digitalocean app. 

To set up a working blog site, just need to do the following steps. 

## Install hugo
```sh
brew install hugo
```

## Create a new site
```sh
hugo new site quickstart
```

## Add a theme
```sh
cd quickstart
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
```

Add the them to the config file.
```sh
echo 'theme = "ananke"' >> config.toml
```

## Add some contents
```sh
hugo new posts/my-first-post.md
```

## Start the test server
```sh
hugo server -D
```

## Customize the site
Modify the config.toml file
```
baseURL = "https://example.org/"
languageCode = "en-us"
title = "My New Hugo Site"
theme = "ananke"
```


## Build static pages
```sh
hugo -D
```
The htmls will be located at `./public`.
