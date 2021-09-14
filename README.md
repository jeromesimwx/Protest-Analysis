# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 4: Group Project


## Overview ##
We will be utilizing The Mass Mobilization (MM), the data mentioned will cover 162 countries on the planet Earth between January 1990 and March 2020. We then classify the data between “aggressive” and “non-aggressive” protests. 


## Background ##
We are the Jedi High Council, peacekeepers of the galaxy. In the past, we’ve spent a lot of time
and resources resolving conflict after it has already occurred. We’ve come to understand that the best way to maintain peace is to pre-empt volatile situations  around  the  galaxy  that  could potentially lead to violent outcomes.


## Problem Statement ##
Governments have a history of varying responses toward different types of protests. We
want to predict the likely government response - specifically, if it is likely to be aggressive to a given protest. Being able to accurately predict this will help us prevent any unnecessary economic losses and threats that may threaten the stability of the region.


## Methodology ##
We will be utilizing The Mass Mobilization (MM), the data mentioned will cover 162 countries on the planet Earth between January 1990 and March 2020. Afterwards, we will train our model using various machine learning techniques to classify whether a protest is aggressive or not.


## Data dictionary ##
1) Unique case identifier 
2) Country name: Polity’s country name. 
3) Country code (Polity code): three-digit Polity Project country code. 
4) Year: 1990- 2020 
5) Region: Regions correspond to Polity code breaks: 
South America – country codes 100-165 
Central America – country codes 40-95 
North America – country codes 20-70 
Europe – country codes 200-390 
Asia – country codes 700-910 
MENA – country codes 600-698 
Africa – country codes 402-590
6) Protest: Is a dichotomous coding for whether or not there was a protest action in a particular period. The project defines a protest as a gathering of 50 or more people to make a demand of the government. 
7) Protest number in year: Represents the number of protests in a year. 
8) Start day: The dates marks the beginning of the protest action. 
9) Start month: The dates marks the beginning of the protest action. 
10) Start year: The dates marks the beginning of the protest action. 
11) End day: The dates mark the ending of the protest action. 
12) End month: The dates mark the ending of the protest action. 
13) End year: The dates mark the ending of the protest action. 
14) Protester violence: Represents whether protesters engaged in violence against the state. 
15) Protest location: Represents the location of the protest as specifically as possible, though specificity varies with reporting. 
16) Number of participants: Represents the estimates of the number of participants at a protest event are notoriously vague and variable. 
17) Protester identity: This variable records the name or identity of the group involved in or organizing the protest. Where possible, it records the hierarchy and identity of the protesters. 
18) Protester demands:
Labor or wage dispute
Land tenure or farm issues
Police brutality or arbitrary actions
Political behavior/processes
Price increases or tax policy
Removal of corrupt or reviled political person
Social restrictions 
19) State responses:
Accommodation of demands
Arrests
Beatings
Ignore
Killings
Shootings
23) Sources: Sources provide an identification of the article(s) used to code the particular protest; notes describe any information that might have informed the coding decision. 
25) Notes: Notes also comment on the facts of the protest events, often quoting from main sources. 


## Brief Summary of Analysis ##
First, we investigated our baseline which was 0.406. We should aim for our models to perform with accuracy rates that are minimally better than this.

We created a base logistic model that seemed to be performing well (AUC = 0.85; Test Accuracy = 0.80) in comparison to our baseline (0.41). The primary concern, however, was our model’s sensitivity score (0.65). Further, while our model performed well in specificity (0.93), this became a cause for concern as the difference between specificity and sensitivity (0.26) was absurdly high, indicating our model’s strong preference toward classifying non-aggressive responses. This problem is especially severe for our purposes as our primary goal was to predict aggressive responses. Therefore, as we moved into hyperparameter tuning, we developed a metric -- Specificity-Sensitivity Balance (henceforth SSB) -- that measures the difference between specificity and sensitivity, scoring a model with a greater number (<1) the lower the difference. Applying SSB to our Logistic Regression model, its score = 0.74.

To obtain the best possible parameters and model, we performed hyperparameter tuning with models: (i) Logistic Regression, (ii) K. Nearest Neighbours Classifier, (ii) Decision Tree Classifier, (iii) Bagging-Decision Tree Classifier, (iv) Bagging-Logistic-Regression Classifier, (v) ADABoost Classifier, and  (vi) Support Vector Machine (SVM) Classifier. Our hyperparameter tuning eventually led us to the conclusion that the best tuned model in predicting both aggressive and non-aggressive responses with a high accuracy was the Bagging-Logistic-Regression Classifier.

Now using a Bagging-Logistic Regression Classifier Model, our test accuracy score is maintained at 0.80. While specificity suffered a fall by 0.02, sensitivity increased by 0.03, meaning that with the hyperparameters at their optimal settings, our model is less able to classify non-aggressive responses, but more able to classify aggressive responses, increasing the SSB to 0.76.


## Findings and Recommendations ##
From our research on The Mass Mobilization (MM) and after modelling, the Bagging-Logistic-Regression classifier serve to be the best model out of all the models tested. 

We analysed the most important features in our Bagging-Logistic-Regression Classifier:

1. In EDA, **participant number** and **protest days** were found to not be highly correlated with aggressive government responses, however, post-modelling, we see that they are among the top 5 more important features in classifying aggressive responses. 

2. A protest's **year** being the second most important feature indicates that it is likely an important factor in determining whether a state's response is aggressive or not. Perhaps on hindsight, we should have performed timeseries analysis to check if aggressive responses follow a trend. 

3. **Protestnumber**, representing the protest the protest number in a country in a year and being an important feature indicates that it becomes more likely a protest is met with an aggressive response when it follows from prior protests in the same country in a given year.

4. **Protest days** being an important feature indicates that it is likely that the longer a protest runs, the more likely it will face an aggressive response.

5. **Removal_of_politician** and **political_behaviour_process** are both politics-related protester demands and represent the top 2 most important demand-related features. This indicates that amongst all the protester demands, protests seeking political change contribute most towards the likelihood of an aggressive government response.

Pulling back to our goal: we want to accurately predict if a given protest on the planet Earth is likely to face an aggressive state response. From feature importance analysis, it seems that the most important features are (in descending order): (i) protesterviolence, (ii) protestnumber, (iii) year, (iv) participantnumber, and (v) protestdays. In fact, protesterviolence is three times more important than protestnumber in our classification process. This means that protesterviolence is likely imperative as a contributor toward an aggressive government response. We therefore recommend that to maximise the efficiency of our preemptive interventions across the galaxy, given our bandwidth, our observers should immediately flag and escalate to the Jedi Council any protests that see its protesters employing violence.


## Limitations ##
1. In our data collection phase, we should collect more data from different sources in order to supplement our current findings. 

2. The overall highest number of protests, 10,750, belongs to the 'political_behavior_process' which is the broadest category and captures aspects of the political process that determines who rules and how, who can participate in elections or decisions, choices made by leaders that influence a range of political outcomes from domestic subsidies to foreign policy. The general category of demanding “reform” would be captured by political behavior or processes, as would demands for democratic transitions. Given its highly political nature, it's also understandable why it also results in the highest number of aggressive government responses: 1,344. The limitation is that we cannot read too deeply into it due to its very broad spectrum of issues which makes it more general than specifically being about a particular group of issues.

3. From our extensive hyperparameter tuning and model experimentation, we find an unchanging inability of every optimally-tuned model to classify aggressive responses as well as non-aggressive responses. We believe that this problem is unresolvable as history simply has not seen an equal number of aggressive and non-aggressive responses, meaning our dataset has far more of the latter than the former.


## Future Steps ##
With social media having an enormous presence in society. A potential future step would be to scrape from sites such as Instagram, Twitter and reddit. With access to a bigger and more recent set of data, we will be able to gain more insights that will allow us to train our model to be better at predictions. 

Potential future projects that we can look towards include a Machine Learning Protest Database System (PDS). This database will function as an automated system with a goal to replace the labor-intensive process of having human coders look for information about protests in news sources with a computer-aided set of protocols. This will help us to overcome the limitation from our research as our research was limited to a short time period. It can also help to overcome the problem of only having one or two news sources available. These practical limits make it difficult to know how general the results from one study will be for other issues or places or time periods.

Another potential future project can be video analysis using OpenCV. With more and more data being video. For example, Tik Tok and Instagram, being able to touch on these sources will be able to provide a bigger picture of what is happening on the ground. With the OpenCV we will be able to do 3 main things: Object Detection, Object Recognition, Object Tracing.