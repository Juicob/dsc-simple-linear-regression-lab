
# Simple Linear Regression - Lab

## Introduction

In this lab, you'll get some hand-on practice developing simple linear regression models. 

## Objectives

You will be able to:

* Perform a linear regression using self-constructed functions
* Interpret the parameters of a simple linear regression model in relation to what they signify for specific data

## Let's get started

The best-fit line's slope $\hat m$ can be calculated as:

$$\hat m = \rho \frac{S_Y}{S_X}$$

With $\rho$ being the correlation coefficient and ${S_Y}$ and ${S_X}$ being the standard deviation of $x$ and $y$, respectively. It can be shown that this is also equal to:

$$\hat m = \dfrac{\overline{x}*\overline{y}-\overline{xy}}{(\overline{x})^2-\overline{x^2}}$$

You'll use the latter formula in this lab. First, break down the formula into its parts. To do this, you'll import the required libraries and define some data points to work with. Next, you'll use some pre-created toy data in NumPy arrays. Let's do this for you to give you a head start. 


```python
# import necessary libraries

import numpy as np
import matplotlib.pyplot as plt
from matplotlib import style
style.use('ggplot')
%matplotlib inline

# Initialize arrays X and Y with given values
# X = Independent Variable
X = np.array([1,2,3,4,5,6,8,8,9,10], dtype=np.float64)
# Y = Dependent Variable
Y = np.array([7,7,8,9,9,10,10,11,11,12], dtype=np.float64)
```


```python
# __SOLUTION__ 
# import necessary libraries

import numpy as np
import matplotlib.pyplot as plt
from matplotlib import style
style.use('ggplot')
%matplotlib inline

# Initialize vectors X and Y with given values
# X = Independent Variable
X = np.array([1,2,3,4,5,6,8,8,9,10], dtype=np.float64)
# Y = Dependent Variable
Y = np.array([7,7,8,9,9,10,10,11,11,12], dtype=np.float64)
```

## Create a scatter plot of X and Y and comment on the output


```python
# Scatter plot

```


```python
# Your observations about the relationship between X and Y 



#
```


```python
# __SOLUTION__ 
# Scatter plot
plt.scatter(X,Y)
```




    <matplotlib.collections.PathCollection at 0x1150111d0>




![png](index_files/index_6_1.png)



```python
# __SOLUTION__ 
# Your observations about relationship in X and Y 

# X is the independent variable or predictor
# Y is The dependent variable or target variable
# The relationship is very linear but not perfectly linear
# The best fit line should be able to explain this relationship with very low error
```

## Write a function `calc_slope()`

Write a function `calc_slope()` that takes in X and Y and calculates the slope using the formula shown above. 


```python
# Write the function to calculate slope as: 
# (mean(x) * mean(y) – mean(x*y)) / ( mean (x)^2 – mean( x^2))
def calc_slope(xs,ys):
    
    pass

calc_slope(X,Y)

# 0.5393518518518512
```


```python
# __SOLUTION__ 
# Write the function to calculate slope as: 
# (mean(x) * mean(y) – mean(x*y)) / ( mean (x)^2 – mean( x^2))
def calc_slope(xs,ys):
    
    # Use the slope formula above and calculate the slope
    m = (((np.mean(xs)*np.mean(ys)) - np.mean(xs*ys)) /
         ((np.mean(xs)**2) - np.mean(xs*xs)))
    
    return m

calc_slope(X,Y)

# 0.5393518518518512
```




    0.5393518518518512



Great, so we have our slope. Next we calculate the intercept. 

As a reminder, the calculation for the best-fit line's y-intercept is:

$$\hat c = \overline y - \hat m \overline x $$


## Write a function best_fit()

Write a function `best_fit()` that takes in X and Y, calculates the slope and intercept using the formula. The function should return slope and intercept values. 


```python
# use the slope function with intercept formula to return calculate slope and intercept from data points

def best_fit(xs,ys):
    
    pass

# Uncomment below to test your function

#m, c = best_fit(X,Y)
#m, c

# (0.5393518518518512, 6.379629629629633)
```


```python
# __SOLUTION__ 
def best_fit(xs,ys):
    
    # use the slope function with intercept formula to return calculate slope and intercept from data points
    m = calc_slope(xs,ys)
    c = np.mean(ys) - m*np.mean(xs)
    
    return m, c

m, c = best_fit(X,Y)
m, c
# (0.5393518518518512, 6.379629629629633)
```




    (0.5393518518518512, 6.379629629629633)



We now have a working model with `m` and `c` as model parameters. We can create a line for the data points using the calculated slope and intercept:

* Recall that $y = mx + c$. We can now use slope and intercept values along with X data points (features) to calculate the Y data points (labels) of the regression line. 

## Write a function reg_line()

Write a function `reg_line()` that takes in slope, intercept and X vector and calculates the regression line using $y= mx + c$ for each point in X


```python
def reg_line (m, c, xs):
    
    pass

# Uncomment below
#regression_line = reg_line(m,c,X)
```


```python
# __SOLUTION__ 
def reg_line (m, c, xs):
    
    return [(m*x)+c for x in xs]

regression_line = reg_line(m,c,X)
```

## Plot the (x,y) data points and draw the calculated regression line for visual inspection


```python
# Plot data and regression line
```


```python
# __SOLUTION__ 
plt.scatter(X,Y,color='#003F72', label="Data points")
plt.plot(X, regression_line, label= "Regression Line")
plt.legend()
```




    <matplotlib.legend.Legend at 0x1074fd5f8>




![png](index_files/index_19_1.png)


So there we have it, our least squares regression line. This is the best fit line and does describe the data pretty well (still not perfect though). 

## Describe your Model Mathematically and in Words


```python
# Your answer here



```


```python
# __SOLUTION__ 
# y = 6.37 + 0.53x

# The line crosses the y-axis at 6.37 (shown in the graph) - intercept
# The slope of the line is 0.53 - a slope 0 would a horizontal line , and slope = 1 would be a vertical one
# Our slope creates an angle roughly around 45 degree between the x and y axes. 
```

## Predicting new data

So, how might you go about actually making a prediction based on this model you just made?

Now that we have a working model with m and b as model parameters. We can fill in a value of x with these parameters to identify a corresponding value of $\hat y$ according to our model. Recall the formula:

$$\hat y = \hat mx + \hat c$$

Let's try to find a y prediction for a new value of $x = 7$, and plot the new prediction with existing data 


```python
x_new = 7
y_predicted = None
y_predicted

# 10.155092592592592
```


```python
# __SOLUTION__ 
x_new = 7
y_predicted = (m*x_new)+c
y_predicted

# 10.155092592592592
```




    10.155092592592592



## Plot the prediction with the rest of the data


```python
# Plot as above and show the predicted value

```


```python
# __SOLUTION__ 

plt.scatter(X,Y,color='#000F72',label='data')
plt.plot(X, regression_line, color='#880000', label='regression line')
plt.scatter(x_new,y_predicted,color='r',label='Prediction: '+ str(np.round(y_predicted,1)))
plt.legend(loc=4)
plt.show()
```


![png](index_files/index_28_0.png)


You now know how to create your own models, which is great! Next, you'll find out how to determine the accuracy of your model!

## Summary

In this lesson, you learned how to perform linear regression for data that are linearly related. You first calculated the slope and intercept parameters of the regression line that best fit the data. You then used the regression line parameters to predict the value ($\hat y$-value) of a previously unseen feature ($x$-value). 
