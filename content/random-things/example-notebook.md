---
title: "Example notebook embedding"
date: 2020-12-11T23:56:51-08:00
draft: false
---


<a href="https://colab.research.google.com/github/Tanu-N-Prabhu/Python/blob/master/Predicting_PewDiePie's_daily_subscribers_using_Machine_Learning_.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

# Predicting PewDiePie's daily subscribers using Machine Learning.

## Let us understand how to predict PewDiePie's daily subscribers using Linear Regression.

![alt text](https://o.aolcdn.com/images/dims?quality=85&image_uri=https%3A%2F%2Fo.aolcdn.com%2Fimages%2Fdims%3Fcrop%3D2999%252C2041%252C0%252C63%26quality%3D85%26format%3Djpg%26resize%3D1600%252C1089%26image_uri%3Dhttp%253A%252F%252Fo.aolcdn.com%252Fhss%252Fstorage%252Fmidas%252Fad4588edcab1d7fb3fcba1779e920b12%252F205651508%252Fauthormedia-personality-pewdiepie-poses-for-a-photo-at-an-book-for-picture-id494847828%26client%3Da1acac3e1b3290917d92%26signature%3D9f9196520c3836b1499e32e6aefbec05a47d1a0e&client=amp-blogside-v2&signature=cd9b8f96b7ccbf8b8546edf04924e2f3d7f95f7a)

[PewDiePie](https://www.youtube.com/channel/UC-lHJZR3Gqxm24_Vd_AJ5Yw) is a Swedish YouTuber and has 100 million subscribers on YouTube (He is my favorite). He gains thousands of subscribers every day, so I thought of writing a tutorial about his gain in subscribers. So I wanted to show you guys a practical implementation of Machine Learning's Linear Regression Algorithm. Here we can apply linear regression to predict his daily YouTube subscribers. I will guide you guys throughout this tutorial how to do so. I will not explain the theory behind linear regression algorithms, because according to me the theory is not so important only the implementation is very important, because you need to know how and where to apply the algorithm. However, I will encourage you to go through some theory online, one of the best articles is shown below:

[Linear Regression](https://towardsdatascience.com/linear-regression-using-python-b136c91bf0a2)



---



# Let's get started:

## The Steps that we are going to follow to complete this implementation is as follows:


1. Importing the necessary libraries.
2. Reading the dataset from the CSV file.
3. Splitting the dataset into independent (x) and dependent (y) variables.
4. Dividing the complete dataset into training and testing dataset.
5. Implement our classifier based on simple linear regression.



## 1: Importing the necessary libraries.


1. numpy
2. pandas 
3. sklearn.linear
4. sklearn.model_selection

**Numpy:** The reason I am using the numpy library is that in the tutorial's ending I'm rounding off some values to get more accurate results. To invoke the round method, I need to import numpy library. To read the official documentation of numpy library visit the link below:

[Numpy](https://numpy.org/devdocs/)

**Pandas:** As you know that I am using the PewDiePie's data from YouTube, I need to store them in some form of a data frame, to store the data in a data frame I am using pandas data frame, it's very easy and interesting to use pandas data frame. To read the official documentation of pandas library visit the link below:

[Pandas:](https://pandas.pydata.org/pandas-docs/stable/)

**Sklearn.linear:** As you know that by now I'm using Linear Regression algorithm to predict the data, I need to import the linear regression library, but you cannot directly import linear regression library, although you need to import sci-kit learn with the help of that you can access linear regression library. That is the reason I'm using sklearn.linear. To read the official documentation of the library visit the link below:

[Sklearn.Linear:](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html) 

**sklearn.model_selection:** If you are implementing linear regression to predict the data, it is often a good practice to divide the data into training and testing data, only then your predicted data would be a lot more accurate. To do this, you need to import model_selection library from scikit learn. To read the official documentation visit the link below:

[Sklearn.model_selection:](https://scikit-learn.org/stable/tutorial/statistical_inference/model_selection.html) 

A quick note to import any library in python all you have to do is just say "import keyword" the keyword can be any name of the library such as pandas, numpy and many more.

**Importing the required libraries for this tutorial is as shown below:**


```
import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
```



---



## 2. Reading the dataset from the CSV file.

I have stored the PewDiePie's subscriber data in a CSV format in Kaggle. Kaggle is a place where people all around the world publish and store the data set. Here I have stored the data in a CSV (Comma Separated Value) format. To download the data set check the link below:

[Data-set: ](https://www.kaggle.com/tanuprabhu/pewdiepies-subscribers)


You can download the data set by clicking the download option. To get the data into a format in python,  you have to use pandas data frame. Now before that you have to load the data into your notebook (I'm using [Google Colab](https://colab.research.google.com/notebooks/welcome.ipynb) to type all my python code), there are multiple ways to load the data into the notebook available online, but the easiest way is in [Google Colab](https://colab.research.google.com/notebooks/welcome.ipynb) at the left-hand side of the notebook, you will find a ">"(greater than symbol). When you click that you will find a tab with three options, you just have to select Files. Then you c an easily upload your file with the help of the Upload option. No need to mount to the google drive or use any specific libraries just upload the data set and your job is done. One thing to remember in this step is that uploaded files will get deleted when this runtime is recycled. This is how I got the data set into the notebook.


```
# Storing the data in a pandas data frame.

df = pd.read_csv("PewDiePie.csv")
df.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Subscribers</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>71915</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>48270</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>47746</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>42276</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>36867</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>28722</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>29794</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>33125</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>27877</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>30675</td>
    </tr>
  </tbody>
</table>
</div>



As you can see the above data set contains two columns, data, and subscribers. I know the date column seems confusing don't worry and think more about it, it's just stored the first day of the May 2019 (like May 1, May 2, and more). And the subscriber's column contains all the subscribers of PewDiePie.



---



## 3. Splitting the dataset into independent (x) and dependent (y) variables.

Before dividing the data set into the train and test data, you need to tell what are dependent and independent variables only then you can divide later. This can be done as follows:


```
x = df.iloc[:, :-1]
y = df.iloc[:, 1]
```

Here the 'x' value comprises the data and the 'y' value comprises the subscribers, and iloc is used to get the values from a data frame. The reason I have used [:,: -1] is because I needed the second last column from the data frame, and the [:1] gives me the last column of the data frame. You can print the value for confirmation.



---



## 4. Dividing the complete dataset into training and testing dataset.

To get a good prediction, divide the data into training and testing data, it is because as the name suggests you will train few data points and test few data points, and keep on doing that unless you get good results.


```
x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = 0.3, random_state = 0)
```

Here both the 'x' and the 'y' variables are divided into training and testing data, as seen in the above code snippet the size of the test data is 0.3 or 30% and the rest is 70% (training data), random_state is the seed used by the random number generator.

Note: Try printing the training values of both x and y, then you will understand what I'm talking about. **HINT: print(x_test)**



---



## 5. Implement our classifier based on simple linear regression.


This is one of the most important because this is where we apply the linear regression algorithm, to do this we have to feed the trained the tested values to the actual algorithm, by doing so we can predict the subscribers. To do this follow the below code:


```
simplelinearRegression = LinearRegression()
simplelinearRegression.fit(x_train, y_train)
```




    LinearRegression(copy_X=True, fit_intercept=True, n_jobs=None, normalize=False)



Here in the above code, we are calling the Linear Regression function and then we are trying to fit the model by-passing the trained values.


```
y_predict = simplelinearRegression.predict(x_test)
```


```
predict = pd.DataFrame(y_predict)
```


```
predict.apply(np.round)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>31042.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>47086.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30098.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>40480.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>38592.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>31985.0</td>
    </tr>
  </tbody>
</table>
</div>



And then we need to predict those values using then predict method, for this we need to pass the tested value of the 'x' variable, by doing so we get the predicted values (subscribers). And the next line of code is just conversion, this is because the y_predict is of type numpy array, so we need to convert this into a data frame only then we can apply the round function. Now the variable predict contains all the predicted subscribers as seen above:

Later I will put the data in a while loop to get it in an actual format, don't worry its just a print statement with the predicted values you will get it once you trace it back down:

This is how the predict function can predict the subscribers, the subscribers returned by the predict function is accurate. Below given is the social blade statistics, you can compare the rest.


```
i = 21
while i <= 28:
  print("Total number of increase in subscribers on May %d ==>" %(i) , int(simplelinearRegression.predict([[i]])))
  i= i+1

```

    Total number of increase in subscribers on May 21 ==> 29154
    Total number of increase in subscribers on May 22 ==> 28210
    Total number of increase in subscribers on May 23 ==> 27266
    Total number of increase in subscribers on May 24 ==> 26322
    Total number of increase in subscribers on May 25 ==> 25378
    Total number of increase in subscribers on May 26 ==> 24434
    Total number of increase in subscribers on May 27 ==> 23491
    Total number of increase in subscribers on May 28 ==> 22547


<a href="http://www.freeimagehosting.net/commercial-photography/"><img src="https://i.imgur.com/gGMEf5i.png" alt="Commercial Photography"></a>

As seen below when you compare the results of the predicted values with the actual subscriber from the above got by Social Blade, the results are almost same except here and there a few more or less subscriber can be found, but that's OK the machine learning cannot predict 100% accurately. Hence this is how you can use Machine Learning Algorithms to predict the daily subscribers of PewDiePie. If you have any doubt about the code, the comment section is all yours. Contact me for doubts only. Thank you guys for reading my article. Bye, start practicing the code and see you next time.



---


