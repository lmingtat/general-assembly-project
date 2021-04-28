# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Mental Health Classification Modelling

### Problem Statement

Currently a lot of travel accomodation services has their own filters when recommending places to stay.
However, these searches are based on the physical traits of the property or rental.
When users do searches on airbnb/hotels in certain areas, they would need to filter by area and read the comments of the place/organisation individually. This usually takes up a lot of time!

Hence, another way that can change this experience is to:
Allows searches based on experiences / user reviews (especially local attractions; Chinatown, LittleIndia, etc..)
Thus, users will be able to read up and search for reviews and location at the same time.

The idea is to build a Named Entity Recognition (NER) model using deep learning, and then compare it to existing pre-trained model to analyse their efficiency, as in how well these models can learn the local areas in Singapore.

### Executive Summary

NER is an information extraction technique to identify and classify named entities within texts. These entities can be pre-defined and generic like peoples' names, organizations, events or they can be very specific like the name of a store. NER has a wide variety of use cases in the business. For example, Gmail applies NER when you are writing an email and you mention a time in your email or attaching a file, gmail offers to set a calendar notification or remind you to attach the file in case you are sending the email without an attachment.

We will be covering the steps taken to clean and analyze the dataset, as well as further steps taken to pre-process the text data before we feed the text into the models. Then, using different models to find the named entities and evaluate our model performance.

The dataset itself is quite clean, but reviews were written in multiple languages, not just in English. Hence, we needed to find away to translate them to English. Then we started off with the available packages, NLTK and spaCy. Then we re-trained the spaCy model with some training set. The main part will be our Bi-LSTM model build in Keras. Because the Airbnb dataset is not pre-annotated, we will use anoter dataset to train it, then following the previous footsteps, we will retrain the model using a small sample of manually annotated training set.  
The performances are then discussed. Refer to below report for our insights, discussions and recommendations.


### Evaluation Findings

**If we ever need to run a model in production, we can consider consider the approach of building your own Bi-LSTM model and re-train it to our specific task at hand**

There seems to be a pattern here as well because the **re-trained** models outperform the un-retrained models.  
This would be an extreme advantage and could even cause the models to become overfitted to our training data.

Not to mention that it is quite difficult to perform a failure analysis on each model on where it tags wrong, this model assessment is not the most accurate way to score each model. However, there is no specific way either in how NLP models are assessed as each models are built and trained very different to each other, and metrics could be misleading.

### Discussions

It is very hard to evaluate each model based on a token-level evaluation. Let's look deeper into the details of each model:

| Model | Data                         | Data Source                                                                                                           | Model Type                 | Entities                                                                                                                              | F1 Score                |
|-------|------------------------------|-----------------------------------------------------------------------------------------------------------------------|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| NLTK  | ACE 2004                     | newswire, broadcast news, telephone conversations                                                                     | MaxEnt classifier          | Organization, Person, Location, Date, Time, Money, Percent, Facility, GPE                                                             | 0.89 ± 0.11 |
| spaCy | OntoNotes                    | telephone conversations, newswire, newsgroups, broadcast news, broadcast conversation, weblogs                        | CNN with GloVe vectors     | Person, Norp, Fac, Org, Gpe, Loc, Product, Event, Work_Of_Art, Law, Language, Date, Time, Percent, Money, Quantity, Ordinal, Cardinal | 0.8585     |
| Bi-LSTM   | GMB (Groningen Meaning Bank) | documents authored by Voice of America VOA, together with documents from the MASC dataset and the CIA World Factbook. | Bi-LSTM with GloVe vectors | Person, GPE, GEO, Organization, Time, Event, Nationality, Art                                                                         | 0.79~0.80               |


Data in table are extracted from [Pahul](https://pahulpreet86.github.io/name-entity-recognition-pre-trained-models-review/). Above only shows the f1 score of our Bi-LSTM model before we re-train it on the Airbnb review dataset.

**Observations**

1. Each model uses different training dataset (each dataset has different sources/backgrounds)
2. Each model uses different architecture (spaCy uses CNN while our model is based on RNNs)
3. Each model has different entity tags (tags can be added when you train the model)
4. Although NLTK has the highest f1 score, followed by spaCy then our Bi-LSTM model, we will not be able to use this as a straight-up comparison because the model build-up is vastly different!

There is a new paper by Jinlan Fu, Pengfei Liu and Graham Neublg from Fudan U. and Carnegie Mellon U..  
It addresses a better way to evaluate different NER models.

Essentially, we can divide the dataset into different categories of entities (as below) and evaluate the models based on each aspect separately. This makes it much easier to identify and quantify where the models perform good or bad.

* Entity Length: String length of the entity
* Sentence Length
* OOV Density: Fraction of ‘Out of Vocabulary’ words in the sentence
* Entity Density: Number of entities in a sentence
* Token Label Consistency: This is a measure of how versatile an entity is.
* Token frequency: How many times the token appears in the dataset
* Entity Label Consistency : Same as Token Label Consistency, but calculated for entity text instead of tokens.
* Entity Frequency : Same as Token Frequency, but calculated for entity text instead of tokens.

We can find out which attributes of the data affect the performance the model, choose the best suited model based on the type of data that you plan to feed it and more importantly know where to apply improvement actions.

**However, this is only for discussion and recommendation for improvement purpose and will not be applied in this project**
    
### Conclusion/Recommendations

Based on our work, we conclude that the re-trained spaCy model works best for predicting named entities from the Airbnb review dataset. However, it might not be the best model in performing NER as a whole.
Each model has its own performance highs and lows, and as such we can consider to fine-tune each model or even re-train them in order to get each model to work for each of our task individually.

#### Further Improvement Recommendation

Below are some of our recommendations on how to improve upon the model:

- Add a CRF (Conditional Random Field) layer after the Bi-LSTM output
    - We wanted to add this but unfortunately Keras has stopped supporting CRF layer
    - There is a TensorflowAddOn for CRF but due to lack of documentation, we do not have enough time to figure it out

- Try other pre-trained embeddings such as Elmo or BERT-like models

- Increase training set
    - As observed above, the total words is more than number of word embeddings, thus some words are not recognised
    - These words will be tagged as OOV and reduces the accuracy of the model
    
- Increase re-training sample size
    - More examples to train on

- Go fully character-based. Eliminate word-level embeddings all together.

- Try out the model evaluation process as written by Jinlan Fu, Pengfei Liu and Graham Neublg
