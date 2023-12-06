---
title: "<p style=\"color: black;\">Text Classification-Naive Bayes from Scratch</p>"
layout: post
---
Problem statement: 

Out Dataset consists of sentences of 6 types ( Responsibility, Requirement, Softskill, Skill, Experience and Education ). We have to classify sentences given to us into these 6 categories. Out Training Dataset consists of sentences and its type which we will feed into the model to learn and then we make our predictions on Test Dataset. 

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t1.png)

                 https://i.stack.imgur.com/uaPM4.png

Naive Bayes learning is known as Supervised Learning since we are feeding data to our model to learn from them. 

<b>Challenge</b>: We will apply Naive Bayes Classifier, not from library, we will build the classifier from scratch. 

Let us dive in. 

<b>Solution:</b> Naive Bayes Classifier assumes that all the data is conditionally independent. This may not be true in some cases of test classification but it gives amazing accuracy while doing text classification.

<b>Naive Bayes Formula : P(A|B) = P(B|A) P(A) / P(B)</b>

A=Sentences, B=Class
We want to find out the probability of a sentence given it is from a specific class.

Let us look at our code.

We begin by doing necessary Imports.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t2.png)

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t3.png)

Let's save our data into DataFrame:

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t4.png)

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t5.png)

We see that our Test Dataset does not have a Type Column so we use it after building our dataset to see which Sentence is predicted as which Type.

We drop null values form our DataFrame:
We see that out dataset size has decreased below

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t6.png)

Plotting Sentence Type and number of sentences of each type:

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t7.png)

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t8.png)

Maximum Sentences of Type Responsibility ( 15257)
Minimum Sentences of Type Education ( 4540 )

<b>Cleaning and Pre-Processing our data:</b>
Remove_punt function is used to remove any HTML tags if any, URLs if any and non-alphanumeric Characters if any. This function is called in our Extraction function to every sentence we have in out Training Dataset.
Extraction function -> we will create a stop words list (imported from nltk) containing Stop Words(English) in general.
We generate a new DataFrame which consists of only the Sentences and their respective Types.
Sequentially, we apply the Remove_punt option mentioned above, convert all sentences to lower case ( <b>And</b> is interpreted differently then <b>and</b>) and then most importantly we lemmatize the words. 
Lemmatization - converting different forms of the word into a single word interpreting the same meaning ( <b>strong, strongly, stronger</b> is interpreted as <b>strong</b>). 

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t9.png)

Our DataFrame size is not affected. Two columns only since we took only sentences and type.


<b>Encoding Type into labels: </b>

Our model understands math instead of words.
![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t10.png)

We have used Sklearn's LabelEncoder to make our work eaiser.
Below is what Type is encoded to which label in our model.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t11.png)

Splitting our Train dataset :

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t12.png)

Transforming words into tokens and building a dictionary of them:

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t13.png)

We import CountVectorizer function from Sklearn and use it to count the number of words and convert them into vectors depending on its frequency.
Vocab consists of only the actual words.
We build w_counts as per the labels given the word. 

<b>Fitting our data:</b>

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t14.png)

We fit our data (X), according to labels ( [0,1,2,3,4,5]). Calculation of prior probability is done for each label.
Let us predict our validation samples and see the accuracy. 

<b>Predicting without Laplace Smoothening-</b>

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t15.png)

White Space Tokenizer is used to split the string into tokens on White space. We buiild our Predict Method to predict the class of the sentence supplied (X_val). For each sentence we are converting them into tokens of words.
We were getting a Math Error because a was becoming 0.
We received the accuracy of 25% on our test set. That is low.
Let us apply Laplace Smoothening.

<b>Predicting with Laplace Smoothening-</b>

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t16.png)

Here, there is not much change from the last Predict Function. We are adding 1 to each word that is not in vocabulary. to save us from math error ( 0 divide by ).

<b>Comparison with Sklearn.NaiveBayes MultinomialNB:</b>
Now Let us compare our model to the one from Library:

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t17.png)

We get an accuracy of 68% from Sklearn's Multinomial Naive Bayes Classifier. 
Let us predict our Test set on both classifiers (One built from Scratch, One from Sklearn Library)

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t19.png)

Preprocessing Test Dataset:

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t20.png)

Since, we have only one column, this function is almost same as the one above for Training Dataset with little details changed.
Let us print first 10 rows from our dataset. 

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t21.png)

Let us compare the predictions from both our models on the above 10 entries from Test set.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t22.png)<-Model from scratch
Model from sklearn -> ![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/t23.png)

We see that out of 10, 7 of the predictions are same in both the Models.

 

Contribution:

1. Comparison of Model Accuracy using Laplace Smoothening.

2. Pre-processing and cleaning the dataset, dropping NA values.

3. Comparison of Model Accuracy of the model built from Scratch and Naive Bayes imported from Sklearn.

4. Comparison of Model Predictions of the models.

5. Increasing Max_features in Counter Vectorizer may result in good performance but it'll take almost 21 minutes to run.


Contribution explanation:

I have used Analytics vidya's Naive Bayes Classifier from Scratch to perform Sentiment Analysis [3] as a reference for Text Classification. We begin by importing the dataset. I have used DataFrame Referencing[2],Lemmatization([4], [1]), Removing Punctuations [5]  to perform Data Pre-preprocessing and Data Cleaning . Then I have used Sklearn's Label Encoder to encode our categorical labels[6]. Usage of count Vectorizer[7] to build the vocabulary and White Space tokenizer[8] to separate the words from sentences for our Predictions.


References:

[1] https://www.analyticsvidhya.com/blog/2022/06/stemming-vs-lemmatization-in-nlp-must-know-differences/ 

[2] https://www.youtube.com/watch?v=8PN1eXQGZ9c&ab_channel=GeeksforGeeks  

[3] https://www.analyticsvidhya.com/blog/2022/03/building-naive-bayes-classifier-from-scratch-to-perform-sentiment-analysis/

[4] https://www.geeksforgeeks.org/python-lemmatization-with-nltk/ 

[5] https://thewebdev.info/2021/10/23/how-to-remove-punctuation-with-python-pandas/

[6] https://scikitlearn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html

[7] https://stackoverflow.com/questions/47898326/how-vectorizer-fit-transform-work-in-sklearn

[8] https://www.educative.io/answers/what-is-whitespacetokenizer-in-python
