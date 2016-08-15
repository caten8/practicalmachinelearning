# Machine Learning: Dumbbell Biceps Curl
Marc Durbin  
August 14, 2016  





## Executive Summary

A Random Forest model classifies data correctly on 20 unknown test cases. Tests with 30 variables achieve a greater than 99% prediction accuracy.

## Background

Using devices such as *Jawbone Up, Nike FuelBand,* and *Fitbit* it is now possible to collect a large amount of data about personal activity relatively inexpensively. These type of devices are part of the quantified self movement – a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. One thing that people regularly do is quantify how much of a particular activity they do, but they rarely quantify how well they do it. In this project, our goal is to use data from accelerometers on the belt, forearm, arm, and dumbbell of six participants who were asked to perform dumbbell lifts correctly and incorrectly in five different ways. More information is available on the Groupware site: [Human Activity Recognition](http://groupware.les.inf.puc-rio.br/har).


## Building the Model(s)

Two models were built, a simple classification algorithm using the LDA method to get a quick look at prediction accuracy and a more complicated multiple technique using the Random Forest method. 


## Cross Validation

Data were grouped into five subgroups using one as the hold-out group while using the other four to train the model. The results were then aggregated to come up with an estimate of the out-of-sample error.


## Out-of-Sample Error Expectations

For our model to perform reliably we need a greater than 95% accuracy to get 20 out of 20. At that level the probability is $0.95^{20} = 0.36$. At 99% it is 0.8. Given the accuracy level achieved via cross-validation against multiple folds, we expect the out-of-sample error rate to be less than 1%. We therefore estimate with 0.936 probability that we can correctly classify all 20.





## LDA Model 

Using k-fold cross validation with five folds.


```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    A    B    C    D    E
##          A 2857  313  182   99   73
##          B   90 1526  189   78  248
##          C  179  297 1424  253  142
##          D  220   71  228 1479  187
##          E    2   72   31   21 1515
## 
## Overall Statistics
##                                           
##                Accuracy : 0.7474          
##                  95% CI : (0.7394, 0.7552)
##     No Information Rate : 0.2843          
##     P-Value [Acc > NIR] : < 2.2e-16       
##                                           
##                   Kappa : 0.6802          
##  Mcnemar's Test P-Value : < 2.2e-16       
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity            0.8533   0.6696   0.6933   0.7663   0.6998
## Specificity            0.9209   0.9363   0.9104   0.9283   0.9869
## Pos Pred Value         0.8107   0.7161   0.6205   0.6769   0.9232
## Neg Pred Value         0.9405   0.9219   0.9336   0.9530   0.9359
## Prevalence             0.2843   0.1935   0.1744   0.1639   0.1838
## Detection Rate         0.2426   0.1296   0.1209   0.1256   0.1287
## Detection Prevalence   0.2993   0.1810   0.1949   0.1855   0.1394
## Balanced Accuracy      0.8871   0.8029   0.8018   0.8473   0.8433
```

LDA Model accuracy overall is 75%, ranging from 67% to 85% in sensitivity. 


## RF Model 

Again, as with LDA, using k-fold cross validation with five folds. 




```
## Loading required package: randomForest
```

```
## randomForest 4.6-12
```

```
## Type rfNews() to see new features/changes/bug fixes.
```

```
## 
## Attaching package: 'randomForest'
```

```
## The following object is masked from 'package:ggplot2':
## 
##     margin
```

```
## Random Forest 
## 
## 11776 samples
##    54 predictor
##     5 classes: 'A', 'B', 'C', 'D', 'E' 
## 
## No pre-processing
## Resampling: Cross-Validated (5 fold) 
## Summary of sample sizes: 9420, 9420, 9423, 9421, 9420 
## Resampling results across tuning parameters:
## 
##   mtry  Accuracy   Kappa    
##    2    0.9904033  0.9878600
##   30    0.9948199  0.9934474
##   58    0.9903188  0.9877532
## 
## Accuracy was used to select the optimal model using  the largest value.
## The final value used for the model was mtry = 30.
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    A    B    C    D    E
##          A 3348    0    0    0    0
##          B    0 2279    0    0    0
##          C    0    0 2054    0    0
##          D    0    0    0 1930    0
##          E    0    0    0    0 2165
## 
## Overall Statistics
##                                      
##                Accuracy : 1          
##                  95% CI : (0.9997, 1)
##     No Information Rate : 0.2843     
##     P-Value [Acc > NIR] : < 2.2e-16  
##                                      
##                   Kappa : 1          
##  Mcnemar's Test P-Value : NA         
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity            1.0000   1.0000   1.0000   1.0000   1.0000
## Specificity            1.0000   1.0000   1.0000   1.0000   1.0000
## Pos Pred Value         1.0000   1.0000   1.0000   1.0000   1.0000
## Neg Pred Value         1.0000   1.0000   1.0000   1.0000   1.0000
## Prevalence             0.2843   0.1935   0.1744   0.1639   0.1838
## Detection Rate         0.2843   0.1935   0.1744   0.1639   0.1838
## Detection Prevalence   0.2843   0.1935   0.1744   0.1639   0.1838
## Balanced Accuracy      1.0000   1.0000   1.0000   1.0000   1.0000
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    A    B    C    D    E
##          A 2231    7    0    0    0
##          B    0 1510    6    0    0
##          C    0    1 1362    3    0
##          D    0    0    0 1283    5
##          E    1    0    0    0 1437
## 
## Overall Statistics
##                                           
##                Accuracy : 0.9971          
##                  95% CI : (0.9956, 0.9981)
##     No Information Rate : 0.2845          
##     P-Value [Acc > NIR] : < 2.2e-16       
##                                           
##                   Kappa : 0.9963          
##  Mcnemar's Test P-Value : NA              
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity            0.9996   0.9947   0.9956   0.9977   0.9965
## Specificity            0.9988   0.9991   0.9994   0.9992   0.9998
## Pos Pred Value         0.9969   0.9960   0.9971   0.9961   0.9993
## Neg Pred Value         0.9998   0.9987   0.9991   0.9995   0.9992
## Prevalence             0.2845   0.1935   0.1744   0.1639   0.1838
## Detection Rate         0.2843   0.1925   0.1736   0.1635   0.1832
## Detection Prevalence   0.2852   0.1932   0.1741   0.1642   0.1833
## Balanced Accuracy      0.9992   0.9969   0.9975   0.9985   0.9982
```

The second algorithm -- the RF Model -- produces reliable results with 30 predictors, reaching an accuracy of 99.5%. 







## Results

The second model using the Random Forest method accurately predicts nearly all of the test cases. The error rate is less than 1%, yielding a .936 probability that the model can classify all 20.  


## Appendix









```r
yvars <- training[,55]
xvars <- training[,-55]
# LDA Model 1
mod1Control <- trainControl(method="cv",number=5,allowParallel=TRUE)
modFit1 <- train(classe ~ .,data=training,method="lda",trControl=mod1Control)
pred1 <- predict(modFit1,training)
confusionMatrix(pred1,training$classe)
```


```r
# RF Model 2
mod2Control <- trainControl(method="cv",number=5,allowParallel=TRUE)
modFit2 <- train(classe ~ .,data=training,method="rf",trControl=mod2Control)
print(modFit2)
pred2 <- predict(modFit2,training)
confusionMatrix(pred2,training$classe)
predicted_test <- predict(modFit2,testing)
confusionMatrix(predicted_test,testing$classe)
```
