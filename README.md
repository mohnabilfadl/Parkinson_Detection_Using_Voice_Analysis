# Prediction of Parkinson’s Disease Using Voice Analysis

# Parkinson’s Disease
Parkinson’s Disease (PD) is a degenerative neurological disorder marked by decreased dopamine levels in the brain. It manifests itself through a deterioration of movement, including the presence of tremors and stiffness. There is commonly a marked effect on speech, including dysarthria (difficulty articulating sounds), hypophonia (lowered volume), and monotone (reduced pitch range). Additionally, cognitive impairments and changes in mood can occur, and risk of dementia is increased.

Traditional diagnosis of Parkinson’s Disease involves a clinician taking a neurological history of the patient and observing motor skills in various situations. Since there is no definitive laboratory test to diagnose PD, diagnosis is often difficult, particularly in the early stages when motor effects are not yet severe. Monitoring progression of the disease over time requires repeated clinic visits by the patient. An effective screening process, particularly one that doesn’t require a clinic visit, would be beneficial. Since PD patients exhibit characteristic vocal features, voice recordings are a useful and non-invasive tool for diagnosis. 
* Source: 'Exploiting Nonlinear Recurrence and Fractal Scaling Properties for Voice Disorder Detection'),Little MA, McSharry PE, Roberts SJ, Costello DAE, Moroz IM.
BioMedical Engineering OnLine 2007, 6:23 (26 June 2007)
> 
# Project Objectives.
This project aims at utilizing machine learning algorithms to detect the presence of the early stage of Parkinson's disease using voice recordings of healthy people and people suffering from parkinson's disease.

# Dataset
The dataset was acquired from kaggle, though it originated from [here](https://archive.ics.uci.edu/ml/machine-learning-databases/parkinsons/), The dataset consists of 195 rows, and 24 columns.The rows represent 195 observations, and the columns represent 23 features and 1 target variable.

Feature	

|Features|Description|
|--------|-----------|
|MDVP:FO(HZ)|Average vocal fundamental frequency|
|MDVP:FHI(HZ)|Maximum vocal fundamental frequency|
|MDVP:FLO(HZ)|Minimum vocal fundamental frequency|
|MDVP:JITTER(%), MDVP:JITTER(ABS),MDVP:RAP,MDVP:PPQ, JITTER:DDP|Several variations in fundamental frequency|
|MDVP:SHIMMER, MDVP:SHIMMER(DB), SHIMMER:APQ3 , SHIMMER:APQ5, MDVP:APQ, SHIMMER:DDA|Several measures of variation in amplitude|
|NHR, HNR|Two measures of ratio of noise to tonal components in the voice|
|STATUS|Health status of the subject (one) - Parkinson's, (zero) - healthy|
|RPDE, D2|Two nonlinear dynamical complexity measures|
|DFA|Signal fractal scaling exponent|
|SPREAD1, SPREAD2, PPE| Three nonlinear measures of fundamental frequency variation|

The distribution of these features varies between individuals with the disease and those without the disease. The orange bars in the barcharts below represents individuals with the disease and the blue bars represents individuals without the disease. There is a clear differnce in the level of voice features in the two groups. This difference is what will be used in the classification of individuals into PD positive and PD negetive status.
![Picture1](https://user-images.githubusercontent.com/95732821/169638157-432b5e67-a6a0-44ab-9f5e-cabdecbcd2d6.png)

A data classification was performed on the above features using KNN,LGBM and XGB classification models. All three models were tuned and evaluated

## Model Evaluation

**Error Types**
In every binary classification problem, there is always a 'positive' class and a 'negative' class. The positive class should be the one you are most interested in findingis usually the group of interest. For this Parkinson's disease dataset, the positive class will be the presence of Parkinson's disease and the negative class will be the absence of parkinson's disease.

**Type 1 error:** If our model predicts the presence of Parkinson's disease, when there is' no disease present, it will have made a type 1 error. This is also known as a false positive.

**Type 2 error:** If our model predicts that there is an absence of Parkinson's disease, when the disease is present, it will have made a type 2 error. This is is also known as a false negative.


### Evaluation Metrics

Accuracy Scores
Accuracy is the metric that is most intuitive.

This is defined as:

![image](https://user-images.githubusercontent.com/95732821/169638957-d64f1e1e-a398-422a-bfe5-afa358dab1af.png)


In other words accuracy is correct predictions the model made out of the total number of predictions.

Pros: Accuracy is easy to understand and gives a combined picture of both kinds of errors in one number.

Cons: Accuracy can be deceiving when a dataset is unbalanced. It also does not give specific information about the kinds of errors that a model is making.

For example,  If the dataset were imbalanced, say 99.9% positive, then a prediction that EVERYTHING is positive would have a very high accuracy. However, that would not be a very useful model for actual medical use. More often we see the opposite: a disease is very rare, occurring .01% of the time or less, and a model that predicts that NO samples ever have the disease will have a high accuracy, but will actually be useless and quite dangerous!

**Recall Scores**
In order to reduce the number of false negatives,the recall scores needs to be improved.

Recall is defined as:
![image](https://user-images.githubusercontent.com/95732821/169638957-d64f1e1e-a398-422a-bfe5-afa358dab1af.png)

It simply asks the question: how many samples did the model label as positive out of all of the true positive samples?

Pros: A higher recall means a fewer false negative predictions, also known as type 2 errors. It's ideal for instances where the classification of a positive as a negative is a costly error.

Cons: Does not consider how many samples |are falsely labeled as positive, or false positives. It does not penalize type 1 errors.

In the case of this dataset, The consequence of predicting a false negative is grevious, as this will prevent the individual seeking for help before the disease reaches the degenerative stage, depriving the individual of a fighting chance against the disease. Therefore it is better to have a model that predicts more false positives than false negatives.  

**Precision Scores**
When the number of false positives needs to be reduced, the precision score is being improved.
Precision is defined as:

![image](https://user-images.githubusercontent.com/95732821/169639653-692b2103-c435-49a9-92b6-d34099f28a9b.png)

In other words: What ratio of the samples predicted in the positive class were truelly in the positive class?

Pros: A high precision means fewer type 1 errors, or fewer false positives. This is a good metric to maximize if a false positive prediction is a costly error.

Cons: Precision does not penalize a model for false negatives. It does not count type 2 errors.

In this case precision would be measuring how many of the individuals diagnosed with Parkinson's disease, actually had the disease.

|KNN Model|	LGBM Model|	XGB Model|
|---------|-----------|----------|
| 	 	![image](https://user-images.githubusercontent.com/95732821/169640422-73155f6e-7fe9-434d-9a25-d9db0c4a980e.png)|![image](https://user-images.githubusercontent.com/95732821/169640438-bf341f1e-ba55-4963-ab45-0e87625bf56a.png)|![image](https://user-images.githubusercontent.com/95732821/169640448-aa088848-f890-493f-843b-9aead9cd885b.png)|
It can be seen here how each model predicted the testing set. The KNN model made about 27% wrong predictions, It predicted the individuals asnegative, when they are actually positive. The LGBM did much better by predicting just about 3% as false negatives, while the XGB model's performance is not as good as the LGB model, it is slightly lower than the KNN, it made 12 false negative predictions.

![image](https://user-images.githubusercontent.com/95732821/169640513-9ee6ba5e-48f2-4f16-81c5-dcf1368ce6b5.png)
The 
![image](https://user-images.githubusercontent.com/95732821/169641860-b60b85c7-8041-4c89-9420-5384cbafe682.png)
![image](https://user-images.githubusercontent.com/95732821/169641883-bc877fd8-dcc8-4043-bca6-9b6672283a90.png)

# Conclusion
All three models performed well on both the train and test set, but LGBM classifier had the highest accuracy score of 97% on the test set, which is just 2.7 less than the 100% score on the train set. Therefore the most suitable model out of all three models for the prediction of early stage parkinson disease in individuals is the LGBM 

# Recommendations
The LGBM Model is reccomended due to having the highest Accuracy, Recall, and Precision Scores.
Accurate prediction can lead to early diagnosis and treatment. Inaccurate prediction can delay diagnosis and treatment, which can be detrimental to the individual.
