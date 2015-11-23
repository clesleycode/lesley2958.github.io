---
layout: post
title: "Getting Started with Natural Language Processing"
tags: NLP DataScience
categories: DataScience
---

<h2> Getting Started with Natural Language Processing </h2>

<h3> Pre-requisites: </h3>

This post assumed some knowledge of Python.

First, install the nltk module:

``` bash
$ pip install nltk
```
<h3> What is Natural Language Processing? </h3>

Natural Language Processing, or NLP, is an area of computer science that focuses on developing techniques used to produce machine-driven analyses of text.

<h3> Why is NLP important? </h3>

NLP expands the sheer amount of data that can be used for insight purposes, since so much of the data we have available is in the form of text.

A specific common application of NLP is each time you use a language conversion tool. The techniques used to accurately convert text from one language to another very much falls under the umbrella of "natural language processing."

<h3> Why is NLP a "hard" problem? </h3>

Language is inheritantly ambiguous. Once person's interpretation of a sentence may very well differ from another person's interpretation. Because of this inability to consistantly be clear, there are no perfect NLP techniques. 

<h3> Regular Expressions: </h3>

<b> Simplest Form: </b> 

The simplest form of a regular expression is a sequence of characters contained within <b>two backslashes</b>. For example, <i>python</i> would be  
``` 
/python/
```

<b> Case Sensitivity: </b>

Regular Expressions are <b>case sensitive</b>, which means 
``` 
/p/ and /P/
```
are distinguishable from eachother. This means <i>python</i> and <i>Python</i> would have to be represented differently, as follows: 

``` 
/python/ and /Python/
```

<b> Disjunctions: </b>

If you want a regular expression to represent both <i>python</i> and <i>Python</i>, however, you can use <b>brackets</b> as the disjunction of the two forms. For example, 
``` 
/[Pp]ython/
```
could represent either <i>python</i> or <i>Python</i>. Likewise, 

``` 
/[0123456789]/
```
would represent a single integer digit. 

<b> Ranges: </b>

If we want a regular expression to express the disjunction of a range of characters, we can use a <b>dash</b>. For example, instead of the previous example, we can write 

``` 
/[0-9]/
```
Similarly, we can represent all characters of the alphabet with 

``` 
/[a-z]/
```

<b> Exclusions: </b>

Brackets can also be used to represent what an expression <b>cannot</b> be if you combine it with the <b>caret</b> sign. For example, the expression 

``` 
/[^p]/
```
represents any character, special characters included, but p.

<b> Question Marks: </b> 

Question marks can be used to represent the expressions containing zero or one instances of the previous character. For example, 

``` 
<i>/colou?r/
```
represents either <i>color</i> or <i>colour</i>. Question marks are often used in cases of plurality. For example, 

``` 
<i>/computers?
```
can be either <i>computers</i> or <i>computer</i>. If you want to extend this to more than one character, you can put the simple sequence within parenthesis, like this:

```
/Feb(ruary)?/
```
This would evaluate to either <i>February</i> or <i>Feb</i>.

``` bash
$ pip install re
```

<h3> Writing your first script: </h3>

``` python
import nltk
```
