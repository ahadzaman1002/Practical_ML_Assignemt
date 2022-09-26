Practical Machine Learning-Week4 Assignment
Ahad Zaman Khan
2022-09-26
Loading and processing The Data
I downloaded the data and reading it from local drive.

library(tidyverse)
list.files()
## [1] "Assignment.R"           "pml-testing.csv"        "pml-training.csv"      
## [4] "Rplot.png"              "week4_assignment.Rmd"   "week4_assignment_cache"
pml_train <- read_csv("pml-training.csv")
First column of the data is row numbers. Lets remove it from the data. I also check how the class variable is distributed.

pml_train <- pml_train[ , -1]

names(pml_train)
##   [1] "user_name"                "raw_timestamp_part_1"    
##   [3] "raw_timestamp_part_2"     "cvtd_timestamp"          
##   [5] "new_window"               "num_window"              
##   [7] "roll_belt"                "pitch_belt"              
##   [9] "yaw_belt"                 "total_accel_belt"        
##  [11] "kurtosis_roll_belt"       "kurtosis_picth_belt"     
##  [13] "kurtosis_yaw_belt"        "skewness_roll_belt"      
##  [15] "skewness_roll_belt.1"     "skewness_yaw_belt"       
##  [17] "max_roll_belt"            "max_picth_belt"          
##  [19] "max_yaw_belt"             "min_roll_belt"           
##  [21] "min_pitch_belt"           "min_yaw_belt"            
##  [23] "amplitude_roll_belt"      "amplitude_pitch_belt"    
##  [25] "amplitude_yaw_belt"       "var_total_accel_belt"    
##  [27] "avg_roll_belt"            "stddev_roll_belt"        
##  [29] "var_roll_belt"            "avg_pitch_belt"          
##  [31] "stddev_pitch_belt"        "var_pitch_belt"          
##  [33] "avg_yaw_belt"             "stddev_yaw_belt"         
##  [35] "var_yaw_belt"             "gyros_belt_x"            
##  [37] "gyros_belt_y"             "gyros_belt_z"            
##  [39] "accel_belt_x"             "accel_belt_y"            
##  [41] "accel_belt_z"             "magnet_belt_x"           
##  [43] "magnet_belt_y"            "magnet_belt_z"           
##  [45] "roll_arm"                 "pitch_arm"               
##  [47] "yaw_arm"                  "total_accel_arm"         
##  [49] "var_accel_arm"            "avg_roll_arm"            
##  [51] "stddev_roll_arm"          "var_roll_arm"            
##  [53] "avg_pitch_arm"            "stddev_pitch_arm"        
##  [55] "var_pitch_arm"            "avg_yaw_arm"             
##  [57] "stddev_yaw_arm"           "var_yaw_arm"             
##  [59] "gyros_arm_x"              "gyros_arm_y"             
##  [61] "gyros_arm_z"              "accel_arm_x"             
##  [63] "accel_arm_y"              "accel_arm_z"             
##  [65] "magnet_arm_x"             "magnet_arm_y"            
##  [67] "magnet_arm_z"             "kurtosis_roll_arm"       
##  [69] "kurtosis_picth_arm"       "kurtosis_yaw_arm"        
##  [71] "skewness_roll_arm"        "skewness_pitch_arm"      
##  [73] "skewness_yaw_arm"         "max_roll_arm"            
##  [75] "max_picth_arm"            "max_yaw_arm"             
##  [77] "min_roll_arm"             "min_pitch_arm"           
##  [79] "min_yaw_arm"              "amplitude_roll_arm"      
##  [81] "amplitude_pitch_arm"      "amplitude_yaw_arm"       
##  [83] "roll_dumbbell"            "pitch_dumbbell"          
##  [85] "yaw_dumbbell"             "kurtosis_roll_dumbbell"  
##  [87] "kurtosis_picth_dumbbell"  "kurtosis_yaw_dumbbell"   
##  [89] "skewness_roll_dumbbell"   "skewness_pitch_dumbbell" 
##  [91] "skewness_yaw_dumbbell"    "max_roll_dumbbell"       
##  [93] "max_picth_dumbbell"       "max_yaw_dumbbell"        
##  [95] "min_roll_dumbbell"        "min_pitch_dumbbell"      
##  [97] "min_yaw_dumbbell"         "amplitude_roll_dumbbell" 
##  [99] "amplitude_pitch_dumbbell" "amplitude_yaw_dumbbell"  
## [101] "total_accel_dumbbell"     "var_accel_dumbbell"      
## [103] "avg_roll_dumbbell"        "stddev_roll_dumbbell"    
## [105] "var_roll_dumbbell"        "avg_pitch_dumbbell"      
## [107] "stddev_pitch_dumbbell"    "var_pitch_dumbbell"      
## [109] "avg_yaw_dumbbell"         "stddev_yaw_dumbbell"     
## [111] "var_yaw_dumbbell"         "gyros_dumbbell_x"        
## [113] "gyros_dumbbell_y"         "gyros_dumbbell_z"        
## [115] "accel_dumbbell_x"         "accel_dumbbell_y"        
## [117] "accel_dumbbell_z"         "magnet_dumbbell_x"       
## [119] "magnet_dumbbell_y"        "magnet_dumbbell_z"       
## [121] "roll_forearm"             "pitch_forearm"           
## [123] "yaw_forearm"              "kurtosis_roll_forearm"   
## [125] "kurtosis_picth_forearm"   "kurtosis_yaw_forearm"    
## [127] "skewness_roll_forearm"    "skewness_pitch_forearm"  
## [129] "skewness_yaw_forearm"     "max_roll_forearm"        
## [131] "max_picth_forearm"        "max_yaw_forearm"         
## [133] "min_roll_forearm"         "min_pitch_forearm"       
## [135] "min_yaw_forearm"          "amplitude_roll_forearm"  
## [137] "amplitude_pitch_forearm"  "amplitude_yaw_forearm"   
## [139] "total_accel_forearm"      "var_accel_forearm"       
## [141] "avg_roll_forearm"         "stddev_roll_forearm"     
## [143] "var_roll_forearm"         "avg_pitch_forearm"       
## [145] "stddev_pitch_forearm"     "var_pitch_forearm"       
## [147] "avg_yaw_forearm"          "stddev_yaw_forearm"      
## [149] "var_yaw_forearm"          "gyros_forearm_x"         
## [151] "gyros_forearm_y"          "gyros_forearm_z"         
## [153] "accel_forearm_x"          "accel_forearm_y"         
## [155] "accel_forearm_z"          "magnet_forearm_x"        
## [157] "magnet_forearm_y"         "magnet_forearm_z"        
## [159] "classe"
length(unique(pml_train$classe))
## [1] 5
unique(pml_train$classe)
## [1] "A" "B" "C" "D" "E"
# find distribution of class variable-
pml_train %>% group_by(classe) %>% 
  summarise( no_obs = n(), prcnt = 100* n()/nrow(.)  )
## # A tibble: 5 × 3
##   classe no_obs prcnt
##   <chr>   <int> <dbl>
## 1 A        5580  28.4
## 2 B        3797  19.4
## 3 C        3422  17.4
## 4 D        3216  16.4
## 5 E        3607  18.4
Lets check for missing values in the data-

# function to check a summary for "NA"s
na_count <-
  function(z) {
    num_obs = nrow(z)
    y =  map_df(z,  ~ sum(is.na(.x)))
    y = pivot_longer(y,
                     everything(),
                     names_to = "variable",
                     values_to = "num_na") %>%
      filter(num_na > 0)
    y$prcnt = y$num_na *100 /num_obs 
    
    return(y)
  }

na_count(pml_train) %>% arrange(-prcnt)
## # A tibble: 100 × 3
##    variable                num_na prcnt
##    <chr>                    <int> <dbl>
##  1 skewness_roll_belt       19225  98.0
##  2 skewness_roll_dumbbell   19220  98.0
##  3 skewness_pitch_dumbbell  19217  97.9
##  4 kurtosis_roll_belt       19216  97.9
##  5 kurtosis_picth_belt      19216  97.9
##  6 kurtosis_yaw_belt        19216  97.9
##  7 skewness_roll_belt.1     19216  97.9
##  8 skewness_yaw_belt        19216  97.9
##  9 max_roll_belt            19216  97.9
## 10 max_picth_belt           19216  97.9
## # … with 90 more rows
100 variables out of 159 variable has 97.93% to 97.97% records are missing “NA”.I am omitting this variables and creating a new data named pml_train2. lets find out which variables does not have missing values:

pml_train2 <- pml_train %>%
  select( -na_count(pml_train)$variable   )
lets find the variables that are not numeric:

pml_train2 %>% select_if(~!is.numeric(.)) %>% names()
## [1] "user_name"      "cvtd_timestamp" "new_window"     "classe"
4 columns are not numerical. “classe” is dependent / predict variable. Ignoring other 3 variables.

pml_train2 <- pml_train2 %>% 
  select( - c("user_name",  "cvtd_timestamp", "new_window") )
Partitioning the data
library(caret)

train_sample <- createDataPartition(y = pml_train2$classe, p = 0.7, list = FALSE)

training <- pml_train2[train_sample,]
testing <- pml_train2[-train_sample,]
Prediction models:
DECISION TREE
DT_model <- train(classe~.,
                  data = training, method = "rpart")

DT_prediction <- predict(DT_model, testing)

confusionMatrix(DT_prediction, as.factor(testing$classe))
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    A    B    C    D    E
##          A 1526  446  476  428  149
##          B   29  407   30  179  164
##          C  115  286  520  357  305
##          D    0    0    0    0    0
##          E    4    0    0    0  464
## 
## Overall Statistics
##                                           
##                Accuracy : 0.4957          
##                  95% CI : (0.4828, 0.5085)
##     No Information Rate : 0.2845          
##     P-Value [Acc > NIR] : < 2.2e-16       
##                                           
##                   Kappa : 0.3413          
##                                           
##  Mcnemar's Test P-Value : NA              
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity            0.9116  0.35733  0.50682   0.0000  0.42884
## Specificity            0.6440  0.91530  0.78123   1.0000  0.99917
## Pos Pred Value         0.5045  0.50309  0.32849      NaN  0.99145
## Neg Pred Value         0.9483  0.85579  0.88238   0.8362  0.88591
## Prevalence             0.2845  0.19354  0.17434   0.1638  0.18386
## Detection Rate         0.2593  0.06916  0.08836   0.0000  0.07884
## Detection Prevalence   0.5140  0.13747  0.26899   0.0000  0.07952
## Balanced Accuracy      0.7778  0.63631  0.64403   0.5000  0.71400
We can see prediction accuracy is only 52.05%.

rpart.plot:: rpart.plot(DT_model$finalModel, 
                        roundint = FALSE)


RANDOM FOREST MDOEL
rm_mdl <- train(classe~., data = training, method = "rf", ntree = 250)

rf_predict <- predict(rm_mdl, testing)
confusionMatrix(rf_predict, factor(testing$classe))
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    A    B    C    D    E
##          A 1674    3    0    0    0
##          B    0 1135    1    0    0
##          C    0    1 1025    3    0
##          D    0    0    0  961    3
##          E    0    0    0    0 1079
## 
## Overall Statistics
##                                           
##                Accuracy : 0.9981          
##                  95% CI : (0.9967, 0.9991)
##     No Information Rate : 0.2845          
##     P-Value [Acc > NIR] : < 2.2e-16       
##                                           
##                   Kappa : 0.9976          
##                                           
##  Mcnemar's Test P-Value : NA              
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity            1.0000   0.9965   0.9990   0.9969   0.9972
## Specificity            0.9993   0.9998   0.9992   0.9994   1.0000
## Pos Pred Value         0.9982   0.9991   0.9961   0.9969   1.0000
## Neg Pred Value         1.0000   0.9992   0.9998   0.9994   0.9994
## Prevalence             0.2845   0.1935   0.1743   0.1638   0.1839
## Detection Rate         0.2845   0.1929   0.1742   0.1633   0.1833
## Detection Prevalence   0.2850   0.1930   0.1749   0.1638   0.1833
## Balanced Accuracy      0.9996   0.9981   0.9991   0.9981   0.9986
Gradient boosting model:
gbm_model <- train(classe~., data = training, method = "gbm", verbose = FALSE )

gbm_model$finalModel
## A gradient boosted model with multinomial loss function.
## 150 iterations were performed.
## There were 55 predictors of which 55 had non-zero influence.
gbm_predict <- predict(gbm_model, testing)

confusionMatrix(gbm_predict, factor(testing$classe))
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    A    B    C    D    E
##          A 1674    3    0    0    0
##          B    0 1135    1    0    0
##          C    0    1 1021    3    0
##          D    0    0    4  957    8
##          E    0    0    0    4 1074
## 
## Overall Statistics
##                                           
##                Accuracy : 0.9959          
##                  95% CI : (0.9939, 0.9974)
##     No Information Rate : 0.2845          
##     P-Value [Acc > NIR] : < 2.2e-16       
##                                           
##                   Kappa : 0.9948          
##                                           
##  Mcnemar's Test P-Value : NA              
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity            1.0000   0.9965   0.9951   0.9927   0.9926
## Specificity            0.9993   0.9998   0.9992   0.9976   0.9992
## Pos Pred Value         0.9982   0.9991   0.9961   0.9876   0.9963
## Neg Pred Value         1.0000   0.9992   0.9990   0.9986   0.9983
## Prevalence             0.2845   0.1935   0.1743   0.1638   0.1839
## Detection Rate         0.2845   0.1929   0.1735   0.1626   0.1825
## Detection Prevalence   0.2850   0.1930   0.1742   0.1647   0.1832
## Balanced Accuracy      0.9996   0.9981   0.9972   0.9952   0.9959
I can see both Random forest and Gradient boosting model are highely accurate. However, Random forest is better performing and I will use this as my prediction model.

LOADING TESTING DATA and cleaning in same manner as test data
pml_test <- read_csv("pml-testing.csv")

pml_test <- pml_test[ ,-1]

pml_test <- pml_test %>% 
  select( -na_count(pml_train)$variable   )

pml_test <- pml_test %>% 
  select( - c("user_name",  "cvtd_timestamp", "new_window") )
Final Prediction:
rf_final_predition <- predict(rm_mdl, pml_test)

rf_final_predition
##  [1] B A B A A E D B A A B C B A E E A B B B
## Levels: A B C D E
