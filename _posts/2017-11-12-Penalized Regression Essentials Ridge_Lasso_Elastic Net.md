---
layout: post
title: Penalized Regression Essentials: Ridge, Lasso & Elastic Net
author: CY
description: "Penalized Regression Essentials: Ridge, Lasso & Elastic Net"
tags: [Machine Learning]
categories: [Machine Learning]
share: false
image:
  background: triangular.png 
---



### Loading required R packages

`tidyverse` for easy data manipulation and visualization                            
`corrplot` for correlations among the variables visualization             
`caret` for easy machine learning workflow                                                 
`glmnet` for computing penalized regression                                            


```r
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(corrplot))
suppressPackageStartupMessages(library(caret))
suppressPackageStartupMessages(library(glmnet))
```



### Preparing the data


```r
# Load the data
data("Boston", package = "MASS")
str(Boston)
```

```
## 'data.frame':	506 obs. of  14 variables:
##  $ crim   : num  0.00632 0.02731 0.02729 0.03237 0.06905 ...
##  $ zn     : num  18 0 0 0 0 0 12.5 12.5 12.5 12.5 ...
##  $ indus  : num  2.31 7.07 7.07 2.18 2.18 2.18 7.87 7.87 7.87 7.87 ...
##  $ chas   : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ nox    : num  0.538 0.469 0.469 0.458 0.458 0.458 0.524 0.524 0.524 0.524 ...
##  $ rm     : num  6.58 6.42 7.18 7 7.15 ...
##  $ age    : num  65.2 78.9 61.1 45.8 54.2 58.7 66.6 96.1 100 85.9 ...
##  $ dis    : num  4.09 4.97 4.97 6.06 6.06 ...
##  $ rad    : int  1 2 2 3 3 3 5 5 5 5 ...
##  $ tax    : num  296 242 242 222 222 222 311 311 311 311 ...
##  $ ptratio: num  15.3 17.8 17.8 18.7 18.7 18.7 15.2 15.2 15.2 15.2 ...
##  $ black  : num  397 397 393 395 397 ...
##  $ lstat  : num  4.98 9.14 4.03 2.94 5.33 ...
##  $ medv   : num  24 21.6 34.7 33.4 36.2 28.7 22.9 27.1 16.5 18.9 ...
```


```r
# data visualization
p.cor<-cor(Boston)
corrplot.mixed(p.cor)
```

![](/images/names-unnamed-chunk-4-1.png)<!-- -->



We'll randomly split the data into training set (80% for building a predictive model) and test set (20% for evaluating the model). Make sure to set seed for reproducibility.

```r
# Split the data into training and test set
set.seed(123)
training.samples <- Boston$medv %>%    #medv is the response variable
                    createDataPartition(p = 0.8, list = FALSE)
# createDataPartition() from "caret" package, split data proportionally

train.data  <- Boston[training.samples, ]
test.data <- Boston[-training.samples, ]
```



input matrix x: This should be created using the function `model.matrix()` allowing to automatically transform any qualitative variables (if any) into dummy variables, which is important because `glmnet()` can only take numerical, quantitative inputs. After creating the model matrix, we remove the intercept component at index = 1.

```r
# Predictor variables
x <- model.matrix(medv~., train.data)[,-1]  

# Response variable
y <- train.data$medv
```



### `cv.glmnet` function         

```
cv.glmnet(x, y, family, lambda, type.measure, nfolds, foldid, grouped, keep, parallel, alpha, ...)

x: input matrix
y: response variable
family: 分布函数。因变量为连续分布(gaussian),因变量为二项分布(binomial)
type.measure: mse(gaussian models) auc(two-class logistic regression), class(binomial and multinomial logistic regression)
nfolds: number of folds - default is 10
```



### k-fold cross-validated ridge regression

```r
# Find the best lambda using cross-validation
set.seed(123) 
cv <- cv.glmnet(x, y, alpha = 0)
# Display the best lambda value (when MSE lowest)
cv$lambda.min
```

```
## [1] 0.7581162
```

```r
# Fit the final model on the training data
ridge <- glmnet(x, y, alpha = 0, lambda = cv$lambda.min)

# Display regression coefficients
coef(ridge)
```

```
## 14 x 1 sparse Matrix of class "dgCMatrix"
##                        s0
## (Intercept)  28.696325628
## crim         -0.072846256
## zn            0.034166905
## indus        -0.057447836
## chas          2.491226902
## nox         -11.092319943
## rm            3.981320544
## age          -0.003137072
## dis          -1.192961128
## rad           0.140678482
## tax          -0.006099569
## ptratio      -0.863997247
## black         0.009365355
## lstat        -0.479141586
```

```r
# Make predictions on the test data
x.test <- model.matrix(medv ~., test.data)[,-1]
predictions <- ridge %>% predict(x.test) %>% as.vector()
# Model performance metrics
data.frame(
  RMSE = RMSE(predictions, test.data$medv),
  Rsquare = R2(predictions, test.data$medv)
)
```

```
##       RMSE  Rsquare
## 1 4.983643 0.671074
```



### k-fold cross-validated LASSO regression

```r
# Find the best lambda using cross-validation
set.seed(123) 
cv <- cv.glmnet(x, y, alpha = 1)
# Display the best lambda value (when MSE lowest)
cv$lambda.min
```

```
## [1] 0.008516101
```

```r
# Fit the final model on the training data
lasso <- glmnet(x, y, alpha = 1, lambda = cv$lambda.min)

# Display regression coefficients
coef(lasso)
```

```
## 14 x 1 sparse Matrix of class "dgCMatrix"
##                        s0
## (Intercept)  36.905385212
## crim         -0.092224281
## zn            0.048424768
## indus        -0.008413932
## chas          2.286235925
## nox         -16.796507506
## rm            3.811860949
## age           .          
## dis          -1.596031128
## rad           0.285461530
## tax          -0.012401417
## ptratio      -0.950408780
## black         0.009646870
## lstat        -0.528799085
```

```r
# Make predictions on the test data
x.test <- model.matrix(medv ~., test.data)[,-1]
predictions <- lasso %>% predict(x.test) %>% as.vector()
# Model performance metrics
data.frame(
  RMSE = RMSE(predictions, test.data$medv),
  Rsquare = R2(predictions, test.data$medv)
)
```

```
##       RMSE   Rsquare
## 1 4.989791 0.6707754
```



### k-fold cross-validated elastic net regression        

The elastic net regression can be easily computed using the `caret` workflow, which invokes the glmnet package.

We use `caret` to automatically select the best tuning parameters `alpha` and `lambda`. The caret packages tests a range of possible alpha and lambda values, then selects the best values for lambda and alpha, resulting to a final model that is an elastic net model.

Here, we'll test the combination of 10 different values for alpha and lambda. This is specified using the option tuneLength.

The best `alpha` and `lambda` values are those values that minimize the cross-validation error

For cross-validated ridge and lasso model, similar codes are used.

```r
# Build the model using the training set
set.seed(123)
elastic <- train(
  medv ~., data = train.data, method = "glmnet",
  trControl = trainControl("cv", number = 10),
  tuneLength = 10
)

# Best tuning parameter
elastic$bestTune
```

```
##    alpha    lambda
## 93     1 0.0170322
```

```r
# Coefficient of the final model. You need to specify the best lambda
coef(elastic$finalModel, elastic$bestTune$lambda)
```

```
## 14 x 1 sparse Matrix of class "dgCMatrix"
##                         1
## (Intercept)  36.256402548
## crim         -0.088577749
## zn            0.046967102
## indus        -0.008012063
## chas          2.269725178
## nox         -16.361460313
## rm            3.829573241
## age           .          
## dis          -1.561700859
## rad           0.271508808
## tax          -0.011838778
## ptratio      -0.944725503
## black         0.009594568
## lstat        -0.529927972
```

```r
# Make predictions on the test data
x.test <- model.matrix(medv ~., test.data)[,-1]
predictions <- elastic %>% predict(x.test)

# Model performance metrics
data.frame(
  RMSE = RMSE(predictions, test.data$medv),
  Rsquare = R2(predictions, test.data$medv)
)
```

```
##       RMSE   Rsquare
## 1 4.986551 0.6710845
```

### repeated k-fold cross-validated elastic net regression  
The process of splitting the data into k-folds can be repeated a number of times, this is called repeated k-fold cross validation.

The final model error is taken as the mean error from the number of repeats.

We generally recommend the (repeated) k-fold cross-validation to estimate the prediction error rate. It can be used in regression and classification settings.

Another alternative to cross-validation is the bootstrap resampling methods, which consists of repeatedly and randomly selecting a sample of n observations from the original data set, and to evaluate the model performance on each copy.

```r
# Build the model using the training set
set.seed(123)
elastic <- train(
  medv ~., data = train.data, method = "glmnet",
  trControl = trainControl(method = "repeatedcv", number = 10, repeats = 3), #10-fold cross validation with 3 repeats
  tuneLength = 10
)

# Best tuning parameter
elastic$bestTune
```

```
##    alpha    lambda
## 54   0.6 0.0393466
```

```r
# Coefficient of the final model. You need to specify the best lambda
coef(elastic$finalModel, elastic$bestTune$lambda)
```

```
## 14 x 1 sparse Matrix of class "dgCMatrix"
##                         1
## (Intercept)  35.513125388
## crim         -0.085096843
## zn            0.045515676
## indus        -0.011769111
## chas          2.270041356
## nox         -15.920104479
## rm            3.850861006
## age           .          
## dis          -1.529248662
## rad           0.253320815
## tax          -0.011020254
## ptratio      -0.936756271
## black         0.009520818
## lstat        -0.529225087
```

```r
# Make predictions on the test data
x.test <- model.matrix(medv ~., test.data)[,-1]
predictions <- elastic %>% predict(x.test)

# Model performance metrics
data.frame(
  RMSE = RMSE(predictions, test.data$medv),
  Rsquare = R2(predictions, test.data$medv)
)  #RMSE lower
```

```
##       RMSE   Rsquare
## 1 4.984612 0.6712767
```


### References   
[Penalized Regression Essentials: Ridge, Lasso & Elastic Net](http://www.sthda.com/english/articles/37-model-selection-essentials-in-r/153-penalized-regression-essentials-ridge-lasso-elastic-net/)        
[Cross-Validation Essentials in R](http://www.sthda.com/english/articles/38-regression-model-validation/157-cross-validation-essentials-in-r/)

























