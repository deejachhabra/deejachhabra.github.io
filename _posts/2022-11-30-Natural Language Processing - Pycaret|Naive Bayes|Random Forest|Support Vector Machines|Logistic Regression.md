---
title:  "<u><p style=\"color: black;\">Natural Language Processing - Pycaret|Naive Bayes|Random Forest|Support Vector Machines|Logistic Regression</p></u>"
layout: post
---

![top](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p1.png)
Image referenced from https://www.formationcomcoach.top/ProductDetail.aspx?iid=149863845&pr=39.88

We have a large product review dataset containing review text, rating and other miscellaneous details. 

<b>Challenge -> Build a text classification model to better classify it as Positive or Negative.</b> 

Let us take a look at what our Data looks like. We are considering review.rating greater than 3 as positive ( 4and 5 ) and review.rating less or equal to 3 as negative.
Sample Text: Had older model, that you could text to speech, this one hasn't. Liked the smaller size, but having to buy a different cover! Still getting used to shelf quite different from my 4 year old model. Paper white is nice reading.
This sample text has a rating of 4 in our Dataset, so we consider it is a positive review.
We will be making one more column, class which has 0 for positive class and 1 for negative class.
We will be using Pycaret first to check which model gives us a better accuracy. 

<b>What is Pycaret?</b>
Pycaret is an open-source, low-code Machine Learning library in Python which automates Machine Learning workflows.
So, basically we spend less time coding and more time on analysis. We just pass our data and it calculated accuracy using every classifier designed for that type of classification. As we move further, we'll get to know how many classifiers are used for Text Classifications below.
Pycaret was developed by the data scientist Moez Ali in the summer of 2019.

Let us dig in!


<b>Pycaret</b>

Necessary Imports-

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p2.png)

Imports for plotting. 

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p3.png)

Spacy is used for Advanced Natural Language Processing in Python and Cython. It comes with pre-trained pipelines and supports Tokenization and Training for 70+ languages. spaCy is commercial open-source software, released under the MIT license.
Some of the tasks handled by spaCy include Tokenization, Lemmatization, Names Entity Recognition, Text Classification.
We will not use spaCy explicitly, but is going to be used in Pycaret.

<b>Data Upload:</b>

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p4.png)

Assigning the data to a DataFrame.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p5.png)

Just a check to see if the data is getting uploaded.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p6.png)

<b>Getting labels </b>
![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p7.png)

We use a function to map the values of the labels to either 0 or 1. 0 is considered to be a Positive Review and 1 is considered to be a Negative Review. 
We are making one more column 'reviews.class' which will have the class label 0 or 1 based on the 'reviews.rating' column. Every review having 'reviews.rating' > 3 is considered to be Positive else Negative.
We have also filled rows having Na values with the Mean of the whole column.
We have stored the text columns in 'data' and labels in 'target'.

<b>Post feature extraction:</b>

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p8.png)

Taking value counts of each class label type ( Number of Positive and Negative Reviews ).

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p9.png)

So, we have 8751 Positive Reviews and 2220 Negative Reviews.

<b>Let us start building. </b>
<b>SETUP function: </b>
setup() function is used to initialize the environment in Pycaret and will perform pre processing on NLP problems. setup must be called before any other function of Pycaret. It takes two parameters-> pandas data frame and a target column which has text to be analyzed. Following Pre - processing steps are applied to the text data.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p10.png)

<b>What is happening in the setup function: </b>
Removing Numerical Characters
Removing Special Characters
Word Tokenization
Stop word Removal
Lemmatizing

Vocab Size -> size of corpus after applying all the preprocessing steps.

<b>Topic Model:</b>
Topic Modelling -> a statistical model for discovering abstract "topics" occurring in group of documents. It is a text mining tool used for discovery of hidden semantic structures in text. Let's say we have Dog and Cat as two topics in our data. So a sentence about dogs will have 'bone', 'dog food' etc. so these words will appear more frequently in documents about dogs rather than the document about cats. 

Why Topic Modelling?
Topic Modelling is used for finding the hidden thematic structures in text. For instance, we have so much unstructured data and to find a way to understand , organize and label this data to make informed decisions.

Creating a Model:
Creating a topic model in Pycaret is simple, we just have to pass the name of the Topic Model we will be using. The name of the model should be passed in String format. We will choose "lda" Latent Dirichlet Allocation model.

<b>Latent-></b> refers to everything we don't know a priori and are hidden in the data.

<b>Dirichlet-></b> It is a Distribution of Distributions i.e distribution of topics in documents and distribution of words in the topic.

<b>Allocation-></b> Once we have Dirichlet, we will allocate topics to documents and words of the documents to topics.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p11.png)

Assigning the Model:
Here we will assign the output of lda to a DataFrame so that we can use the setup function from Pycaret. Post this, there are additional columns added for each topic in our DataFrame, the dominant topic, 'en' the text field, Percentage of Dominant Topic over other topics etc.
Note: Creating and Assigning Model might take some time.

<b>Plot Models:</b>
Topic Model  -> Lets plot the above created Topic Model. It has divided our data into 4 topics. Lets check the model.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p12.png)

It is an interactive Model. We can select any one of the topics and it'll give us their contribution in a particular word. or in other words, it'll let us know the contribution of a word into a particular topic.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p13.png)

I have selected Topic 1 here. You are welcome to play with it in the notebook. This one is just a static image. 

	2. WordCloud -> ![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p14.png)

Word Cloud is similar to the one which we normally use. It is a data visualization technique for representing text data in which size of each word indicates its frequency or importance. "The bigger the word the more frequent it is".

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p15.png)

From the above Word Cloud we can easily understand that most of the reviews are positive. This is true as we saw in value counts calculation. And mostly there are ear accessories like headphones, apple bud etc. 

What we have:
![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p16.png)

We will remove text and rating as Pycaret does not take that as Input. We already have our numerical features (class, topics). 

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p17.png)

Let us setup out model again with the above dataframe. Previous one had text, but in this one we grouped words of texts into topics.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p18.png)

We are ready to compare models now. 

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p19.png)

Sorting models using Accuracy as a metric. 

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p20.png)

We have the output from Pycaret Text Classification. As can be seen from the above output, we get accuracy of every classifier, we just had to pass our data and it calculated the accuracy using each above mentioned classifer. Hence, low code.
We see that Random Forest Classifier gives us the highest accuracy here of about 85% and Naive Bayes and Quadratic Discriminant Analysis of 77% and 35% respectively.
Let us try some of the classifiers above to check how much accuracy do they give using our Traditional Model Building Approach. 

<b>Traditional Model Building</b>

Let us split the dataset into training and validation dataset.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p21.png)

<b>Naive Bayes Classifier</b>

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p22.png)
picture referenced from https://towardsdatascience.com/introduction-to-na%C3%AFve-bayes-classifier-fa59e3e24aaf

Naive Bayes Classifier is based on Bayes Theorem that is, every feature is independent of other features given the class variable.
In practice, we take interest in only the numerator of the fraction, as the denominator does not depend on the class.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p23.png)

Our Accuracy using Naive Bayes is 84% compared to Pycaret's 72%.
Let us try some other model too. 

<b>Random Forest Classifier</b>

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p24.png)
picture referenced from  https://builtin.com/data-science/random-forest-algorithm

To best explain Random Forest Classifier, lets see an example. My friend wants to decide where to go for vacation and asks me for suggestions. I in turn ask him about the likes and dislikes of his past travels. Based on his answers I am applying a Decision Tree Approach with two subtrees as Likes and Dislikes. This is Decision Tree. What is my friend asks 10 people the same question. Then he'll pick up the majority answer from all the ten people's suggestions. This is Random Forest Classifier. ( A bunch of friends giving the same answer based on two classes likes and dislikes )

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p25.png)

It is also more than what Pycaret has predicted. 
Here we are basically converting our sentences to a matrix of token counts. We fit our model and predict using our Validation set. The accuracy we get is 90% compared to Pycaret's 85%.

<b>Support Vector Machines</b>

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p26.png)
picture referenced from  https://ai-pool.com/a/s/understanding-of-support-vector-machine--svm

SVM generates hyperplane which segregates the classes in the best way. Support Vectors are the nearest points to the hyperplane from either side. These help in separating the line better by calculating margins. Support Vectors are data points which are closest to the hyperplane. Margin is the gap between the point and the hyperplane on either side of the classification. So for linear classification like in our case, it'll have two support vectors. 

Imports

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p27.png)

WordNetLemmatizer-> Lemmatization

nltk -> stopwords, wordnet, punkt

re-> regular expression for data pre processing

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p28.png)


Created a Data preprocessing function to remove links, 
everything except alpha numeric characters, 
lemmatizing and tokenization, 
in the end joining the tokens together and returning it.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p29.png)

Here we pre processed the data first and then converted into matrix of tokens using which we create BOW -> Bag of Words . Using the new bag of words we split the dataset into Xtrain, Xtest, ytrain, ytest amd use it to fit and predict our model.
We got an accuracy of 88% using SVM compared to Pycaret's 81%.


<b>Logistic Regression</b>

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p30.png)

Logistic Regression has a logistic function which looks like a big S and will transform any value between 0 and 1 shows above. So we can say if val passed from logistic function and the value now is < 0.5 then it can be considered as Class 0 else Class 1.

Logistic Function - 

Logistic function models the exponential growth of a population, but also puts a limit on the growth. eg from 0 to 1.


![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p31.png)
											reference- https://mathequalslove.net/12-basic-functions-posters/	
                                            
![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p32.png)

Logistic Regression gave an accuracy of 89% compared to Pycaret's 77%.


Let us compare each model 
We are plotting bar plot to compare accuracies. 
![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p33.png)
![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p34.png)

The best accuracy is given by RFC ( Random Forest Classifier ) as Pycaret predicted. The lowest accuracy is of Naive Bayes Classifier, what Pycaret predicted.
all the classifiers we have used above give accuracies above 80%. Surprisingly, Naive Bayes classifier which is supposed to be the best for Text Classification gives the lowest accuracy amongst all the classifiers we have used.

<b>Final Testing :</b>
It is time to test our X_test with the final classifier model. [Random Forest Classifier]

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p35.png)
Lets print some of the samples and their classified review class.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/p36.png)

this is what we got. Each review is correctly classified except the second one "Medium Quality" which is classified as Positive but should not have been.
Additionally, we got an accuracy of 91% which is pretty good.


Video for this project can be found at YouTube at the below link, go check it out!
https://youtu.be/bCXEF57pwJI 


Contribution-> 

Pycaret Library Research. 

Digging and research on various types of classifiers used in Traditional Model Building.

Comparison of accuracies at the end of the blog.

Word Cloud formation in Pycaret to detect which words are more frequent.

Topic Model Plot to visualize which words contribute to which amongst the four topics and how much.

Traditional Model Building.

Understanding Pycaret Framework.

Getting to understand SETUP(), COMPARE_MODELS(), PLOT(), TOPIC MODELLING etc. from Pycaret Library.

Notebook->

DM_Main_1001990775_final
.ipynb
Download IPYNB • 585KB



References -> 

1. https://www.geeksforgeeks.org/how-to-fill-nan-values-with-mean-in-pandas/
filling null  values

2. https://www.geeksforgeeks.org/create-a-new-column-in-pandas-dataframe-based-on-the-existing-columns/
# creating a new column based on rating column

3. https://stackoverflow.com/questions/38255796/pandas-round-is-not-working-for-dataframe
# rounding off values to nearest integer

4. https://www.kaggle.com/code/ohseokkim/fake-news-easy-nlp-text-classification 
# Building-Model

5. https://stackoverflow.com/questions/56927602/unable-to-load-the-spacy-model-en-core-web-lg-on-google-colab
# spacy module download

6. https://medium.com/@tenzin_ngodup/simple-text-classification-using-random-forest-fe230be1e857
# text classification Random forest classifier

7. https://www.kaggle.com/code/mehmetlaudatekman/text-classification-svm-explained
# svm text classification

8. https://kavita-ganesan.com/news-classifier-with-logistic-regression-in-python/#.Y3zpl3bMLIU
# Logistic Regression

9. https://pycaret.gitbook.io/docs/learn-pycaret/official-blog/nlp-text-classification-in-python-using-pycaret
# pycaret setup

10. https://pycaret.readthedocs.io/en/latest/api/nlp.html
# pycaret setup official documentation

11. https://pycaret.org/
# pycaret

12. https://www.google.com/search?q=pycaret+founder&rlz=1C1UEAD_enIN975IN975&oq=pycaret+founder&aqs=chrome..69i57j0i390l5.5850j0j4&sourceid=chrome&ie=UTF-8
# pycaret origin

13. https://pycaret.gitbook.io/docs/
# pycaret

14. https://towardsdatascience.com/5-things-you-are-doing-wrong-in-pycaret-e01981575d2a
# pycaret moez ali

15. https://github.com/explosion/spaCy/blob/master/README.md
# Spacy

16. https://medium.com/analytics-vidhya/topic-modeling-using-lda-and-gibbs-sampling-explained-49d49b3d1045
# lda pycaret

17. https://towardsdatascience.com/5-things-you-are-doing-wrong-in-pycaret-e01981575d2a
# lda pycaret

18. https://github.com/pycaret/pycaret 
# pycaret notebooks

19. https://github.com/pycaret/pycaret 
# pycaret official documentation

20. https://pycaret.readthedocs.io/en/latest/api/classification.html 
# pycaret classification
