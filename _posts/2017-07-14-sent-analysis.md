---
layout: post
title: Sentiment Analysis with Messy Data
tags: datascience education
categories: datascience education 
---

# Sentiment Analysis with Messy Data

So you might be asking, what exactly is "sentiment analysis"?

Well, it's exactly what it sounds like: it's using computational tools to determine the emotional tone behind words. This is important because it allows you to gain an understanding of the attitudes, opinions, and emotions of the people in your data. 

At a higher level, sentiment analysis involves Natural Language Processing and artificial intelligence by taking the actual text element, transforming it into a format that a machine can read, and using statistics to determine the actual sentiment.

In this tutorial, we'll introduce the Natural Language Processing module, [nltk](http://www.nltk.org/), to determine the sentiment of tweets from [Twitter](https://twitter.com/). 

Sentiment Analysis isn't a new concept. There are thousands of labeled data out there, labels varying from simple positive and negative to more complex systems that determine how positive or negative is a given text. Because there’s so much ambiguity within how textual data is labeled, there’s no one way of building a sentiment analysis classifier.

With that said, I've selected a pre-labeled set of data consisting of tweets from Twitter already labeled as positive or negative. Using this data, we'll build a sentiment analysis model with nltk.


## Environment Setup

This guide was written in Python 3.6. If you haven't already, download [Python](https://www.python.org/downloads/release/python-361/) and [Pip](https://pypi.python.org/pypi/pip). Next, you’ll need to install the nltk package that we’ll use throughout this tutorial:

```
pip3 install nltk==3.2.4
```

Since we’ll be working with Python interactively, using the [Jupyter Notebook](http://jupyter.readthedocs.io/en/latest/install.html) is the best way to get the most out of this tutorial. Once you have your notebook up and running, you can [download](https://github.com/lesley2958/twilio-sent-analysis) the data we'll be working with in this example. You can find this in the repo as negative_tweets and positive_tweets. Make sure you have the data in the same directory as your notebook and then we’re good to go! 

## A Quick Note on Jupyter

For those of you who are unfamiliar with Jupyter notebooks, I’ve provided a brief review of which functions will be particularly useful to move along with this tutorial. 
In the image below, you’ll see three buttons labeled 1-3 that will be important for you to get a grasp of -- the save button (1), add cell button (2), and run cell button (3). 

[PICTURE NEEDS TO GO HERE]

The first button is the button you’ll use to **save your work** as you go along (1). I won’t give you directions as when you should do this -- that’s up to you! 

Next, we have the **“add cell”** button (2). Cells are blocks of code that you can run together. These are the building blocks of jupyter notebook because it provides the option of running code incrementally without having to run all your code at once.  Throughout this tutorial, you’ll see lines of code blocked off -- each one should correspond to a cell. 

Lastly, there’s the “run cell” button (3). Jupyter Notebook doesn’t automatically run your code for you; you have to tell it when to do it by clicking "run cell". As with the add button, once you’ve written each block of code in this tutorial onto your cell, you should then run it to see the output (if any). If any output is expected, note that it will also be shown in this tutorial so you know what to expect. *Make sure to run your code as you go along because many blocks of code in this tutorial rely on previous cells.* 


## Preparing the Data

We'll now use nltk to build a sentiment analysis model on the same dataset. `nltk` requires a different data format, which is why I've implemented the function below:


```python
import nltk

def format_sentence(sent):
return({word: True for word in nltk.word_tokenize(sent)})

print(format_sentence("The cat is very cute"))
```

{'The': True, 'cat': True, 'is': True, 'very': True, 'cute': True}


Here, `format_sentence()` changes each tweet into a dictionary of words mapped to True booleans. Though not obvious from this function alone, this will eventually allow us to train our prediction model by splitting the text into its tokens, i.e. *tokenizing* the text. You'll learn about why this format is important in a later section.

Using the data we downloaded from the github repo, we'll format the positively and negatively labeled data.


```python
pos = []
with open("./pos_tweets.txt") as f:
for i in f: 
pos.append([format_sentence(i), 'pos'])

neg = []
with open("./neg_tweets.txt") as f:
for i in f: 
neg.append([format_sentence(i), 'neg'])
```

Next, we'll split the labeled data into the training and test data, just as we did before.


```python
training = pos[:int((.8)*len(pos))] + neg[:int((.8)*len(neg))]
test = pos[int((.8)*len(pos)):] + neg[int((.8)*len(neg)):]
```

## Building a Classifier

All `nltk` classifiers work with feature structures, which can be simple dictionaries mapping a feature name to a feature value. In this example, we use the [Naive Bayes Classifier](http://www.nltk.org/_modules/nltk/classify/naivebayes.html), which makes predictions based on the word frequencies associated with each label of positive or negative.



```python
from nltk.classify import NaiveBayesClassifier

classifier = NaiveBayesClassifier.train(training)
```

Since the Naive Bayes Classifier is based entirely off of the frequencies associated with each label for a given word, we can call a function `show_most_informative_features()` to see which words are the highest indicators of a positive or negative label:


```python
classifier.show_most_informative_features()
```

Most Informative Features
no = True              neg : pos    =     19.4 : 1.0
love = True              pos : neg    =     19.0 : 1.0
awesome = True              pos : neg    =     17.2 : 1.0
headache = True              neg : pos    =     16.2 : 1.0
Hi = True              pos : neg    =     12.7 : 1.0
beautiful = True              pos : neg    =      9.7 : 1.0
Thank = True              pos : neg    =      9.7 : 1.0
fan = True              pos : neg    =      9.7 : 1.0
New = True              pos : neg    =      9.7 : 1.0
haha = True              pos : neg    =      9.3 : 1.0


Notice that there are three columns. Column 1 is why we used `format_sentence()` to map each word to a True value. What it does is count the number of occurrences of each word for both labels to compute the ratio between the two, which is what column 3 represents. Column 2 lets us know which label occurs more frequently. The label on the left is the label most associated with the corresponding word.

## Classification

Just to see how our model works, let's try the classifier out with a positive example:


```python
example1 = "Cats are awesome!"

print(classifier.classify(format_sentence(example1)))
```

pos


Now let's try out an example we'd expect a negative label:


```python
example2 = "I don’t like cats."

print(classifier.classify(format_sentence(example2)))
```

neg


So what happens when we mix words of different sentiment labels? Let's take a look at this example:


```python
example3 = "I have no headache!"

print(classifier.classify(format_sentence(example3)))
```

neg


And we've found a mislabel! Naive Bayes doesn't consider the relationship between words, which is why it wasn't able to catch the fact that "no" acted as a negator to the word headache. Instead, it read two negative indicators and classified it as such.
Given that, we can probably expect a less than perfect accuracy rate.


```python
y_pred = log_model.predict(X_test)
```

## Accuracy

nltk has a built in method that computes the accuracy rate of our model:


```python
from nltk.classify.util import accuracy
print(accuracy(classifier, test))
```

0.8308457711442786


`nltk` specializes and is *made for* natural language processing tasks, so we should expect that nltk do fairly well with uncleaned and unnormalized data. But why has this well established models only resulted in ~80% accuracy rates? It goes back to the lack of processing beforehand.

If you look at the actual data, you'll see that the data is kind of messy - there are typos, abbreviations, grammatical errors of all sorts. There’s no general format to every tweet aside from the fact that each tweet is, well, a tweet. So what can we do about this? 

For now, we’re stuck with our 83% accurate classifier. 

If you liked what you did here, [follow me](https://twitter.com/lesleyclovesyou) (@lesleyclovesyou) on Twitter for more content, data science ramblings, and most importantly, retweets of super cute puppies.
