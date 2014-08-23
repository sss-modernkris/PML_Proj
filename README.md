## Problem Statement:

Using devices such as Jawbone Up, Nike FuelBand, and Fitbit it is now possible to collect a large amount of data about personal activity relatively inexpensively. These type of devices are part of the quantified self movement - a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. One thing that people regularly do is quantify how much of a particular activity they do, but they rarely quantify how well they do it. In this project, our goal will be to use data from accelerometers on the belt, forearm, arm, and dumbell of 6 participants. They were asked to perform barbell lifts correctly and incorrectly in 5 different ways. More information is available from the website here: http://groupware.les.inf.puc-rio.br/har (see the section on the Weight Lifting Exercise Dataset). 


The goal of our project is to predict the manner in which they did the exercise. This is the "classe" variable in the training set. 

- Any of the other variables can be used to predict "classe"  
- Create a report describing how the model is built  
- how cross validation is done?  
- what is the expected out of sample error? 
- Justification for the choices made.   
- Use resultant prediction model to predict 20 different test cases.  


## 1. Synopsis  

Loaded the data from .csv files. After exploring the data, since there are lots of blanks and NA in the certain columns
decided to remove those columns. Some of the columns are not relavent for the problem. So

1. Excluded from the training set all columns which are consistently blank/NA.
2. Excluded the first 7 columns from the training set (columns: record ID, user name, timestamps, new_window, and num_window) since any predictive value from these features will presumably *not* apply out of sample. 

This left me with 52 predictors: roll_belt through magnet_forearm_z.

Then the training data was split into a training set and a cross validation set (using a 75%/25% split) so that latter accuracy can be estimated with independent data set that is different from training set.

Using the train function in the caret package, I tried a few different models (pls - partial least squares method, rda - regularized discriminant model, rf - random forest) with different trade-offs of simplicity, interpretability, and accuracy. For all of these models, I used simple 10-fold cross-validation with no repetitions rather than the default bootstrap method, both to reduce computational cost and to simplify the explanation of my cross-validation strategy (as requested by the assignment). Not surprisingly, I ultimately settled on a random forest model with default settings. The train function selected mtry=2, since this has very good accuracy, it took almost an hour on 3.5GHz, i7 computer.

Cross-validation accuracy in the training set I constructed is  ~100%. Accuracy on the test set I constructed was 99.5%. Finally, pridicted the classe for the test data using the final random forest model.

Results files were generated and submitted with 100% correct classification.
