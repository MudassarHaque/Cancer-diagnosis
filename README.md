# Personalized cancer diagnosis
Source: https://www.kaggle.com/c/msk-redefining-cancer-treatment/

## Business Problem

Description:

Data: Memorial Sloan Kettering Cancer Center (MSKCC)

Download training_variants.zip and training_text.zip from Kaggle.

Context:
Source: https://www.kaggle.com/c/msk-redefining-cancer-treatment/discussion/35336#198462

Problem statement : 
Classify the given genetic variations/mutations based on evidence from text-based clinical literature.

## Source/Useful Links
Some articles and reference blogs about the problem statement

https://www.forbes.com/sites/matthewherper/2017/06/03/a-new-cancer-drug-helped-almost-everyone-who-took-it-almost-heres-what-it-teaches-us/#2a44ee2f6b25
https://www.youtube.com/watch?v=UwbuW7oK8rk
https://www.youtube.com/watch?v=qxXRKVompI8
2.3  1.3. Real-world/Business objectives and constraints.
No low-latency requirement.
Interpretability is important.
Errors can be very costly.
Probability of a data-point belonging to each class is needed.

## Machine Learning Problem Formulation

### Data Overview
Source: https://www.kaggle.com/c/msk-redefining-cancer-treatment/data
We have two data files: one conatins the information about the genetic mutations and the other contains the clinical evidence (text) that human experts/pathologists use to classify the genetic mutations.
Both these data files are have a common column called ID
Data file's information:

## Mapping the real-world problem to an ML problem

### Type of Machine Learning Problem
There are nine different classes a genetic mutation can be classified into => Multi class classification problem

### Performance Metric
Source: https://www.kaggle.com/c/msk-redefining-cancer-treatment#evaluation

### Metric(s):

Multi class log-loss
Confusion matrix
###  Machine Learing Objectives and Constraints
Objective: Predict the probability of each data-point belonging to each of the nine classes.

### Constraints:

Interpretability * Class probabilities are needed. * Penalize the errors in class probabilites => Metric is Log-loss. * No Latency constraints.

### Train, CV and Test Datasets
Split the dataset randomly into three parts train, cross validation and test with 64%,16%, 20% of data respectively
training_variants (ID , Gene, Variations, Class)
training_text (ID, Text)


### results 


|  model   |      train loss     |      cv loss       |     test loss      |  %age misclassified |
| :-: | :-: | :-: | :-: | :-: |
|    NB    |  0.5808981140522917 | 1.2489160815466813 | 1.160798379861729  | 0.39849624060150374 |
|   knn    |  0.5013965550403059 | 1.071069394962044  | 0.9801894745981695 |  0.3966165413533835 |
|  lr_CB   | 0.43620619239652675 | 1.0446418765377858 | 0.9267087369787624 | 0.37218045112781956 |
| lr_NOCB  | 0.42477117052638386 | 1.042513516689416  | 0.9260032223829916 | 0.37406015037593987 |
|   SVM    |  0.4938179976414916 | 1.1570228659400166 | 1.0362669483902183 |  0.3684210526315789 |
|  RF_OHE  |  0.5730631458709511 | 1.128655240958627  | 1.0795427719378035 | 0.37030075187969924 |
|  RF_RC   |  0.0632807011252621 | 1.226273297845348  | 1.137636626543795  |  0.4191729323308271 |
| Stacking |  0.5866235148652802 | 1.2078647727110252 | 1.0975912337086096 |  0.3443609022556391 |
|  Voting  |  0.7902691169035738 | 1.1994693380665884 | 1.1083444707122763 |  0.3398496240601504 |

### conclusions
 In this case study we have very high cost of error so for every model we should look for mis classfication percentage which matters most when cost of error is high

Linear models like Logistic regression perform well enough to reduce log-loss for test data

Voting classifier gives less %age of misclassified points

so we can clearly see that out cv_dataset and train_dataset have many outliers apart from test_dataset 
In a pervious instance of splitting dataset gave me 30% misclassified points in LR with .93 cv and .92 test loss 
in this situation we can try to remove noise from dataset to make model perform much more efficent.
