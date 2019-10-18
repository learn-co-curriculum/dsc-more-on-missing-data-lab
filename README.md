
# More on Missing Data - Lab

## Introduction

In this lab, you'll continue to practice techniques for dealing with missing data. Moreover, you'll observe the impact on distributions of your data produced by various techniques for dealing with missing data.

## Objectives

In this lab you will: 

- Evaluate and execute the best strategy for dealing with missing, duplicate, and erroneous values for a given dataset   
- Determine how the distribution of data is affected by imputing values 

## Load the data

To start, load the dataset `'titanic.csv'` using pandas.


```python
# Your code here

```


```python
# __SOLUTION__ 
# Your code here
import pandas as pd
df = pd.read_csv('titanic.csv')
df.head()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>0.0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>1.0</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>1.0</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>1.0</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>0.0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



Use the `.info()` method to quickly preview which features have missing data


```python
# Your code here

```


```python
# __SOLUTION__ 
# Your code here
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1391 entries, 0 to 1390
    Data columns (total 12 columns):
    PassengerId    1391 non-null float64
    Survived       1391 non-null float64
    Pclass         1391 non-null object
    Name           1391 non-null object
    Sex            1391 non-null object
    Age            1209 non-null float64
    SibSp          1391 non-null float64
    Parch          1391 non-null float64
    Ticket         1391 non-null object
    Fare           1391 non-null float64
    Cabin          602 non-null object
    Embarked       1289 non-null object
    dtypes: float64(6), object(6)
    memory usage: 130.5+ KB


## Observe previous measures of centrality

Let's look at the `'Age'` feature. Calculate the mean, median, and standard deviation of this feature. Then plot a histogram of the distribution.


```python
# Your code here

```


```python
# __SOLUTION__ 
# Your code here
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

print(df['Age'].apply(['mean', 'median', 'std']))
df['Age'].hist()
```

    mean      29.731894
    median    27.000000
    std       16.070125
    Name: Age, dtype: float64





    <matplotlib.axes._subplots.AxesSubplot at 0x11bdacd30>




![png](index_files/index_9_2.png)


## Impute missing values using the mean 

Fill the missing `'Age'` values using the average age. (Don't overwrite the original data, as we will be comparing to other methods for dealing with the missing values.) Then recalculate the mean, median, and std and replot the histogram.


```python
# Your code here

```


```python
# __SOLUTION__ 
# Your code here
age_na_mean = df['Age'].fillna(value=df['Age'].mean())
print(age_na_mean.apply(['mean', 'median', 'std']))
age_na_mean.hist()
```

    mean      29.731894
    median    29.731894
    std       14.981155
    Name: Age, dtype: float64





    <matplotlib.axes._subplots.AxesSubplot at 0x11ec35a90>




![png](index_files/index_12_2.png)


### Commentary

Note that the standard deviation dropped, the median was slightly raised and the distribution has a larger mass near the center.

## Impute missing values using the median 

Fill the missing `'Age'` values, this time using the media age. (Again, don't overwrite the original data, as we will be comparing to other methods for dealing with the missing values.) Then recalculate the mean, median, and std and replot the histogram.


```python
# Your code here

```


```python
# __SOLUTION__ 
# Your code here
age_na_median = df['Age'].fillna(value=df['Age'].median())
print(age_na_median.apply(['mean', 'median', 'std']))
age_na_median.hist()
```

    mean      29.374450
    median    27.000000
    std       15.009476
    Name: Age, dtype: float64





    <matplotlib.axes._subplots.AxesSubplot at 0x11edc73c8>




![png](index_files/index_16_2.png)


### Commentary

Imputing the median has similar effectiveness to imputing the mean. The variance is reduced, while the mean is slightly lowered. You can once again see that there is a larger mass of data near the center of the distribution.

## Dropping rows

Finally, let's observe the impact on the distribution if we were to simply drop all of the rows that are missing an age value. Then, calculate the mean, median and standard deviation of the ages along with a histogram, as before.


```python
# Your code here

```


```python
# __SOLUTION__ 
# Your code here
age_na_dropped = df[~df['Age'].isnull()]['Age']
print(age_na_dropped.apply(['mean', 'median', 'std']))
age_na_dropped.hist()
```

    mean      29.731894
    median    27.000000
    std       16.070125
    Name: Age, dtype: float64





    <matplotlib.axes._subplots.AxesSubplot at 0x11eebe0f0>




![png](index_files/index_20_2.png)


### Commentary

Dropping missing values leaves the distribution and associated measures of centrality unchanged, but at the cost of throwing away data.

## Summary

In this lab, you briefly practiced some common techniques for dealing with missing data. Moreover, you observed the impact that these methods had on the distribution of the feature itself. When you begin to tune models on your data, these considerations will be an essential process of developing robust and accurate models.
