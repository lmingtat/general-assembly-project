# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Mental Health Classification Modelling

### Problem Statement

The National Council of Social Service (NCSS) has contacted us on one emerging issue revolving around mental health, with more and more people taking initiative to contact NCSS for support especially during the COVID-19 period. The NCSS believes that although there has been an increase in public participation, there are a lot of people who are not aware of their condition and some might be reluctant to acknowledge their condition.

**We are consulted to come up with a classification model that will enable NCSS to judge the condition of anyone in the community based on their social media posts, specifically if any person in question suffers from depression.**

This will allow the social workers to quickly identify people who needs help, and with earlier medication and support, there can be better impact onto the livelihood of the affected community, or anyone in Singapore.

<u>Why is this important?</u> [Samaritans of Singapore](https://www.sos.org.sg/learn-about-suicide/quick-facts)
 - Suicide is the leading cause of death for those aged 10-29
 - There are 3 times more deaths from suicide than transport accidents in 2019
 - 400 lives were lost to suicide in 2019
 - For every suicide, at least 6 suicide survivors are left behind


### Executive Summary

Nowadays there are so many social media applications that anyone can flock to, and comes in different forms or formats. However, to solve our problem, we intend to apply Natural Language Processing (NLP) technique, and this requires huge amounts of text. The best application that we can think of is Reddit! Reddit is a social news platform that allows users to discuss and vote on content that other users have submitted.

Our chosen subreddits are:
* r/depression
* r/love  

Obviously, people who are depressed will gather under r/depression and the opposite (positive) people would go to r/love.

We will be covering the steps taken to clean and analyze the data collected, as well as further steps taken to pre-process the text data, visualize the data, use different models to find the optimal model and evaluate our model performance.

The first thing we did was to import our data using the Reddit API, and proceed to clean up duplicates and sticky posts. Once done, an explratory data analysis was conducted to identify any trends between most frequently used words. Data visualisation using barplots, WordClouds and venn diagrams greatly helped to point out further insights. We also did a sentiment analysis on our featured texts to see if the posts are helpful to solve our problem.   
Then comes our modelling process. We started off with 8 models and based on our model's accuracy, we cut down to 2 models for further evaluation. Our model evaluation will include other metrics (other than accuracy) that are important to our question, if someone is predicted to be depressed or not. Based on our metric score, we picked on 1 last model to be used as our production classification model. Refer to below report for our insights and recommendations.

**Overall Report Structure**
1. Problem Statement
2. Reddit API
3. Data Cleaning and EDA
4. Visualisation and Analysis
5. Modelling Selection, Optimization, Evaluation
6. Conclusion & Recommendations

### Data Dictionary

Modelling Process:

| Model Labels | Full Labels              |
|:-----------:|:------------------------:|
| cvec        | CountVectorizer          |
| tvec        | TFidVectorizer           |
| logreg      | LogisticRegression       |
| nb          | NaiveBayes (Multinomial) |
| rf          | RandomForest             |
| ada         | AdaBoost                 |
| xgc         | XGBoost                  |


### Evaluation Findings

| Model | Accuracy Score              |
|:-----------:|:---------------------:|
| Logistic        |     0.907      |
| Multinomial NB  | 0.912        |

Based on our initial modelling process, we observe that the Multinomial NaiveBayes classifier (with CountVec), 0.912 and LogisticRegression classifier (with TFidfVec), 0.907 has the top2 highest validation score, meaning that they are more accurate in predicting unseen data.
We will pick and use these 2 models in our model evaluation process.

Although our 2 models above have a higher accuracy score compared to other types of classifiers, we will need to further evaluate between models.  
Reason is because accuracy only tells us more about our True positive and True negative. Yes, it is important that we can classify correctly our samples (accuracy), but we also need to look at other performance metrics.

We will visit back our problem statement for this part, where we want to correctly predict if someone has depression or not.  
In truth, the cost of our type1 error and type2 error is different (false positive and false negative are not equal!).  

- <span style='color:blue'> <span>False positive (someone who does not have depression but was classified as depressed)
- <span style='color:blue'> <span>False negative (**someone who is depressed but was misclassified as not depressed!**)

As we can see above, our false negative has a much higher cost (human life) compared to our false positive. At most, the affected person will be taking some form of medication but not life threatening.
    
**Since our False Negatives are so important (and our model accuracy is high enough >90%), we will look into our recall.**  
Theoretically, we want to maximise our recall.  
    Recall — Out of all the depressed people, how many are predicted as depressed?
    
| Model | Recall Score              |
|:-----------:|:-------------------:|
| Logistic        |     0.919      |
| Multinomial NB  | 0.914        |

Our NaiveBayes model has the upper hand in accuracy (+0.05) but our LogReg model has the upper hand in recall (+0.05)!

For reasons discussed above, it will be wiser to pick the Logistic model as our production model. We want to maximise our recall score, and in our context (using our holdout set), this means 1x more people who are depressed classified as not depressed. The cost might be unimaginable!  
    
### Conclusion/Recommendations

During our EDA, one of our observations was that our text features are not very good in helping us perform classification (not much difference). However, during our modelling process, we see that this thought is not valid as our models are minimally above 80% accuracy. This is very important to note because our EDA might not provide the final picture before we build our models.
Building our classifier model needs to take into account several aspects and metrics, notably recall for our topic. Our final production model chosen is the Multinomial NaiveBayes with CountVectorizer. This model gave us the highest accuracy and highest recall score.  
For our problem at hand, we can say that our model will be enable NCSS to judge accurately up to 91.2% (whoever has depression), albeit our correct positive predictions stand at 91.4% (8.6% chance that we might misclassify someone with depression).  
    
Now that we have our model, we will also be able to tell what words are the most useful in predicting if someone has depression: 'help','bad','work','cannot','anything','fuck','need','start','everything','live'  
Thus, someone who frequently uses these words (or words that lemmatize to these) would generally have a higher chance to be depressed.

#### Further Improvement Recommendation

[1] Consider evaluating using other metrics, precision, F1-score  
During our evaluation process, we predominantly looked at only 2 metrics, our accuracy and recall(sensitivity). However, in a wider context, all metrics are important too, such as precision and specificity. For the sake of highlighting our cost of type2 error (false negative), we focus more on recall in our analysis.
For example, precision tells us - out of all people that we predict as depressed, how many are really depressed?
In general, we can look to F1 score for a better overall model performance evaluation

[2] Adding more words into our stopwords list  
We observed that there are actually quite a lot of words that has high frequency, but were not actually important. Thus, we can consider to add these words into our stopword list and perhaps try to reduce overfitting to the training set, although it's not our main focus.
