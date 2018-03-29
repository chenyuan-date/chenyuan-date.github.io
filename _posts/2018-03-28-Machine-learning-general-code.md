---
layout: post
title: Machine Learning General Codes (R and Python)
author: CY
tags: [Python]
categories: [Python]
share: false
image:
  background: triangular.png
---



source: [Analytisc vidhya](https://www.analyticsvidhya.com/)



## Machine learning 

- Supervised Learning                                      
  - Decision Tree                                                     
  - Random Forest                                
  - kNN      
  - SVM
  - Naive-Bayes                                                
  - Logistic Regression          
  - linear Regression                                                                   
- Unsupervised Learning                       
  - Apriori algorithm                           
  - PCA                                    
  - k-means                                          
  - Hierarchical Clustering                          
  - Hidden Markov Model                           
- Reinforcement Learning                    
  - Markov Decision Process                 
  - Q Learning                 




## Linear Regression

### Python code 

```
#Import Library
#Import other necessary libraries like pandas, numpy...
from sklearn import linear_model
#Load Train and Test datasets
#Identify feature and response variable(s) and values must be numeric and numpy arrays
x_train=input_variables_values_training_datasets
y_train=target_variables_values_training_datasets
x_test=input_variables_values_test_datasets
#Create linear regression object
linear = linear_model.LinearRegression()
#Train the model using the training sets and check score 
linear.fit(x_train, y_train)
linear.score(x_train, y_train)
#Equation coefficient and Intercept
print('Coefficient: \n', linear.coef_)
print('Intercept: \n', linear.intercept_)
#Predict Output
predicted= linear.predict(x_test)
```

### R code

```
#Load Train and Test datasets
#Identify feature and response variable(s) and values must be numeric and numpy arrays
x_train <- input_variables_values_training_datasets
y_train <- target_variables_values_training_datasets
x_test <- input_variables_values_test_datasets
x <- cbind(x_train,y_train)
#Train the model using the training sets and check score
linear <- lm(y_train ~ ., data = x)
summary(linear)
#Predict Output
predicted= predict(linear, x_test)
```



## Logistic Regression

### Python code 

```
#Import Library
from sklearn.linear_model import LogisticRegression
#X(predictor) and Y(target) for training data set and x_test(predictor) for test_dataset
#Create logistic regression object
model = LogisticRegression()
#Train the model using the training sets and check score
model.fit(X, y)
model.score(X, y)
#Equation coefficient and Intercept
print('Coefficient: \n', model.coef_)
print('Intercept: \n', model.intercept_)
#Predict Output
predicted= model.predict(x_test)
```

### R code 

```
x <- cbind(x_train,y_train)
#Train the model using the training sets and check score
logistic <- glm(y_train ~ ., data = x,family='binomial')
summary(logistic)
#Predict Output
predicted= predict(logistic,x_test)
```



## Decision Tree

### Python code 

```
#Import Library
#Import other necessary libraries like pandas, numpy...
from sklearn import tree
#X(predictor) and Y(target) for training data set and x_test(predictor) for test_dataset
#Create tree object 
model = tree.DecisionTreeClassifier(criterion='gini') 
#for classification, here you can change the algorithm as gini or entropy (information gain) by 
#default it is gini 
#model = tree.DecisionTreeRegressor() for regression
#Train the model using the training sets and check score
model.fit(X, y)
model.score(X, y)
#Predict Output
predicted= model.predict(x_test)
```

### R code 

```
#Import Library
library(rpart)
x <- cbind(x_train,y_train)
#grow tree 
fit <- rpart(y_train ~ ., data = x,method="class")
summary(fit)
#Predict Output 
predicted= predict(fit,x_test)
```

 

## SVM (Support Vector Machine)

### Python code 

```
#Import Library
from sklearn import svm
#X(predictor) and Y(target) for training data set and x_test(predictor) for test_dataset
#Create SVM classification object 
model = svm.svc() 
#there are various options associated with it, this is simple for classification. 
#Train the model using the training sets and check score
model.fit(X, y)
model.score(X, y)
#Predict Output
predicted= model.predict(x_test)
```

### R code 

```
#Import Library
library(e1071)
x <- cbind(x_train,y_train)
#Fitting model
fit <-svm(y_train ~ ., data = x)
summary(fit)
#Predict Output 
predicted= predict(fit,x_test)
```



## Naive Bayes

### Python code 

```
#Import Library
from sklearn.naive_bayes import GaussianNB
#X(predictor) and Y(target) for training data set and x_test(predictor) for test_dataset
#Create SVM classification object 
model = GaussianNB() 
#there is other distribution for multinomial classes like Bernoulli Naive Bayes
#Train the model using the training sets and check score
model.fit(X, y)
#Predict Output
predicted= model.predict(x_test)
```

### R code 

```
#Import Library
library(e1071)
x <- cbind(x_train,y_train)
#Fitting model
fit <-naiveBayes(y_train ~ ., data = x)
summary(fit)
#Predict Output 
predicted= predict(fit,x_test)
```



## kNN (k-Nearest Neighbors)

### Python code 

```
#Import Library
from sklearn.neighbors import KNeighborsClassifier
#X(predictor) and Y(target) for training data set and x_test(predictor) for test_dataset
#Create K Neighbors classifier object model 
KNeighborsClassifier(n_neighbors=6) 
#default value for n_neighbors is 5
#Train the model using the training sets and check score
model.fit(X, y)
#Predict Output
predicted= model.predict(x_test)
```

### R code 

```
#Import Library
library(knn)
x <- cbind(x_train,y_train)
#Fitting model
fit <-knn(y_train ~ ., data = x,k=5)
summary(fit)
#Predict Output 
predicted= predict(fit,x_test)
```



## k-Means

### Python code 

```
#Import Library
from sklearn.cluster import KMeans
#X(predictor) and Y(target) for training data set and x_test(predictor) for test_dataset
#Create KNeighbors classifier object model 
k_means = KMeans(n_clusters=3, random_state=0)
#Train the model using the training sets and check score
model.fit(X)
#Predict Output
predicted= model.predict(x_test)
```

### R code 

``` 
#Import Library
library(cluster)
fit <- kmeans(X, 3) 
#5 cluster solution
```



## Random Forest

### Python code 

```
#Import Library
from sklearn.ensemble import RandomForestClassifier
#X(predictor) and Y(target) for training data set and x_test(predictor) for test_dataset
#Create Random Forest object
model = RandomForestClassifier()
#Train the model using the training sets and check score
model.fit(X, y)
#Predict Output
predicted= model.predict(x_test)
```

### R code 

```
#Import Library
library(randomForest)
x <- cbind(x_train,y_train)
#Fitting model
fit <- randomForest(Species ~ ., x,ntree=500)
summary(fit)
#Predict Output 
predicted= predict(fit,x_test)
```



## Dimensionality Reduction Algorithms

### Python code 

```
#Import Library
from sklearn import decomposition
#Assumed you have training and test data set as train and test
#Create PCA object 
pca = decomposition.PCA(n_components=k) 
#default value of k =min(n_sample, n_features) 
#For Factor analysis
# fa = decomposition.FactorAnalysis()
#Reduced the dimension of training dataset using PCA
train_reduced = pca.fit_transform(train)
#Reduced the dimension of test dataset
test_reduced = pca.transform(test)
```

### R code 

```
#Import Library
library(stats)
pca <- princomp(train, cor = TRUE)
train_reduced <- predict(pca,train)
test_reduced <- predict(pca,test)
```



## Gradient Boosting & AdaBoost

### Python code 

```
#Import Library
from sklearn.ensemble import GradientBoostingClassifier
#X(predictor) and Y(target) for training data set and x_test(predictor) for test_dataset
#Create Gradient Boosting Classifier object
model = GradientBoostingClassifier(n_estimators=100, \ 
learning_rate=1.0, max_depth=1, random_state=0)
#Train the model using the training sets and check score
model.fit(X, y)
#Predict Output
predicted= model.predict(x_test)
```

### R code 

```
#Import Library
library(caret)
x <- cbind(x_train,y_train)
#Fitting model
fitControl <- trainControl( method = "repeatedcv", 
+ number = 4, repeats = 4)
fit <- train(y ~ ., data = x, method = "gbm", 
+ trControl = fitControl,verbose = FALSE)
predicted= predict(fit,x_test,type= "prob")[,2]
```



