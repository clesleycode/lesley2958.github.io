---
layout: post
title: "Getting Started with Natural Language Processing"
tags: NLP DataScience 
categories: DataScience
---

<h2> Getting Started with Natural Language Processing </h2>

<h3> Pre-requisites: </h3>

This post assumes some knowledge of Python.

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

If you want a regular expression to represent both <i>python</i> and <i>Python</i>, however, you can use <b>brackets</b> or the <b>pipe</b> symbol as the disjunction of the two forms. For example, 
``` 
/[Pp]ython/ or /Python|python/
```
could represent either <i>python</i> or <i>Python</i>. Likewise, 

``` 
/[0123456789]/ 
```
would represent a single integer digit. The pipe symbols are typically used for interchangable strings, such as in the following example:

```
/dog|cat/
```

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

<b> Kleene Star: </b>

To represent the expressions containing zero or <b>more</b> instances of the previous character, we use an <b>asterisk</b> as the kleene star. To represent the set of strings containing <i>a, ab, abb, abbb, ...</i>, the following regular expression would be used:  
```
/ab*/
```

<b> Wildcards: </b>

Wildcards are used to represent the possibility of any character and symbolized with a <b>period</b>. For example, 

```
/beg.n/
```
From this regular expression, the strings <i>begun, begin, began,</i> etc., can be generated. 

<b> Kleene+: </b>

To represent the expressions containing at <b>least</b> one or more instances of the previous character, we use a <b>plus</b> sign. To represent the set of strings containing <i>ab, abb, abbb, ...</i>, the following regular expression would be used:  

```
/ab+
```

<h3> N-Grams: </h3>

<b> What is an n-gram? </b>

An n-gram is a sequence of n items from a specific text or corpus.



