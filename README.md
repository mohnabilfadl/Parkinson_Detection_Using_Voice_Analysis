# Prediction of Parkinson’s Disease Using Voice Analysis

![parkinson2](https://user-images.githubusercontent.com/63733989/170835549-b2456085-24b4-4f2a-848d-9fb24cde2301.jpg)

# Parkinson’s Disease:
Parkinson’s Disease (PD) is a degenerative neurological disorder marked by decreased dopamine levels in the brain. It manifests itself through a deterioration of movement, including the presence of tremors and stiffness. There is commonly a marked effect on speech, including dysarthria (difficulty articulating sounds), hypophonia (lowered volume), and monotone (reduced pitch range). Additionally, cognitive impairments and changes in mood can occur, and risk of dementia is increased.

Traditional diagnosis of Parkinson’s Disease involves a clinician taking a neurological history of the patient and observing motor skills in various situations. Since there is no definitive laboratory test to diagnose PD, diagnosis is often difficult, particularly in the early stages when motor effects are not yet severe. Monitoring progression of the disease over time requires repeated clinic visits by the patient. An effective screening process, particularly one that doesn’t require a clinic visit, would be beneficial. Since PD patients exhibit characteristic vocal features, voice recordings are a useful and non-invasive tool for diagnosis. 
* Source: 'Exploiting Nonlinear Recurrence and Fractal Scaling Properties for Voice Disorder Detection'),Little MA, McSharry PE, Roberts SJ, Costello DAE, Moroz IM.
BioMedical Engineering OnLine 2007, 6:23 (26 June 2007)
> 
# Project Objectives:
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


## Model Evaluation

**Error Types**
In every binary classification problem, there is always a 'positive' class and a 'negative' class. The positive class should be the one you are most interested in findingis usually the group of interest. For this Parkinson's disease dataset, the positive class will be the presence of Parkinson's disease and the negative class will be the absence of parkinson's disease.

**Type 1 error:** If our model predicts the presence of Parkinson's disease, when there is' no disease present, it will have made a type 1 error. This is also known as a false positive.

**Type 2 error:** If our model predicts that there is an absence of Parkinson's disease, when the disease is present, it will have made a type 2 error. This is is also known as a false negative.


### Evaluation Metrics

Accuracy Scores
Accuracy is the metric that is most intuitive.

This is defined as:

![image](https://user-images.githubusercontent.com/63733989/170835692-eea27661-fdee-40d9-956a-a6e5451421a3.png)


In other words accuracy is correct predictions the model made out of the total number of predictions.

Pros: Accuracy is easy to understand and gives a combined picture of both kinds of errors in one number.

Cons: Accuracy can be deceiving when a dataset is unbalanced. It also does not give specific information about the kinds of errors that a model is making.

For example,  If the dataset were imbalanced, say 99.9% positive, then a prediction that EVERYTHING is positive would have a very high accuracy. However, that would not be a very useful model for actual medical use. More often we see the opposite: a disease is very rare, occurring .01% of the time or less, and a model that predicts that NO samples ever have the disease will have a high accuracy, but will actually be useless and quite dangerous!

**Recall Scores**
In order to reduce the number of false negatives,the recall scores needs to be improved.

Recall is defined as:

![image](https://user-images.githubusercontent.com/63733989/170835748-f26bfb28-a1af-4506-aa2b-20b110b8ed7c.png)

It simply asks the question: how many samples did the model label as positive out of all of the true positive samples?

Pros: A higher recall means a fewer false negative predictions, also known as type 2 errors. It's ideal for instances where the classification of a positive as a negative is a costly error.

Cons: Does not consider how many samples |are falsely labeled as positive, or false positives. It does not penalize type 1 errors.

In the case of this dataset, The consequence of predicting a false negative is grevious, as this will prevent the individual seeking for help before the disease reaches the degenerative stage, depriving the individual of a fighting chance against the disease. Therefore it is better to have a model that predicts more false positives than false negatives.  

**Precision Scores**
When the number of false positives needs to be reduced, the precision score is being improved.
Precision is defined as:

![image](https://user-images.githubusercontent.com/63733989/170835723-fbf6fc7b-d9e1-4671-968b-d9064287d92a.png)

In other words: What ratio of the samples predicted in the positive class were truelly in the positive class?

Pros: A high precision means fewer type 1 errors, or fewer false positives. This is a good metric to maximize if a false positive prediction is a costly error.

Cons: Precision does not penalize a model for false negatives. It does not count type 2 errors.

In this case precision would be measuring how many of the individuals diagnosed with Parkinson's disease, actually had the disease.

# Models Final results 

![res](https://user-images.githubusercontent.com/63733989/170835524-e00411d6-70b0-40cb-857e-29cef41362d1.png)


# Conclusion

* We can conclude that SVM && kNN Model are best for our dataset as they are giving highest AUC score.
* The higher the AUC, the better the performance of the model at distinguishing between the positive and negative classes.
* Hence we will make Prediction System for SVM Model and save this model into pickle file.
