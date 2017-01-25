---
layout: post
title:  Trends and Semantics of Inaugural Speeches 
author: <a href="http://chandlerzuo.github.io/">Chandler</a>
---

As the new president delivered his inaugural speech just 4 days ago, one additional entry was been added to the American Inaugural Address Database. As a diligent data scientist, I could not help ask this question: across the history, what are the trends and patterns of inaugural speeches?

Of course, asking about trends and patterns is too broad an analytical task. Therefore, for my analysis I focus on the following questions:

1. How does the level of linguistic complexity has changed across the history?
2. Which presidents have similar semantic patterns in their inaugural addresses?

Answering this question leads to an NLP exercise that I am sharing in this post. As the input data, I found a download [link](https://archive.org/details/Inaugural-Address-Corpus-1789-2009) containing inaugural addresses until 2009, and added to this data set by the 2013 and 2017 addresses that can be downloaded from anywhere.

**LINGUISTIC COMPLEXITY**

To analyze the linguistic complexity, I computed the following metrics for each inaugural address:

1. Number of sentences;
2. Average number of words in each sentence;
3. Average word length;
4. Average constituency parse tree depth;
5. [Flesch-Kincaid Grade Level](https://en.wikipedia.org/wiki/Flesch%E2%80%93Kincaid_readability_tests).

The first three metrics are naive. The constituency parse tree depth describes the syntactic complexity of a sentence. Constituency parse tree describes how different elements in a sentence are syntactically related to each other. Usually the depth of this tree is correlated with a sentence, but not necessarily. The deeper this tree is, the more nested syntactic components are there within the sentence. Take for example, a sample sentence from George Washington's address has the following parse tree:

![](https://dl.dropboxusercontent.com/u/72368739/blog/inaugural/stgraph_washington.png =200x)

While a sample sentence from the new president's address has the following structure:

![](https://dl.dropboxusercontent.com/u/72368739/blog/inaugural/stgraph_trump.png)

Flesch-Kincaid Grade Level aggregates the length of sentences, length of words, and number of syllabus to describe the overall content difficulty of a text passage. The output number, K, means that the text is suitable for a common student in Grade K.

I computed all scores by using python's NLTK, Stanford CoreNLP and textstat modules. I then produced figures to represent how each metric changed across the years. And here are the results:

![](https://dl.dropboxusercontent.com/u/72368739/blog/inaugural/num_of_sentences.png)
![](https://dl.dropboxusercontent.com/u/72368739/blog/inaugural/sentence_length.png)
![](https://dl.dropboxusercontent.com/u/72368739/blog/inaugural/word_length.png)
![](https://dl.dropboxusercontent.com/u/72368739/blog/inaugural/parse_tree_depth.png)
![](https://dl.dropboxusercontent.com/u/72368739/blog/inaugural/flesch_kincaid.png)

It is interesting that the number of sentences is the only metric that have almost no pattern. The length of the address has changed a lot across the history. All other metrics suggest a trend of decay in the linguistic complexity. The new inaugural address set a record on the simplicity in the syntactic structures, but its sentence shortness was beaten by Johnson, and its average word length was way above the record set by JFK's final term.

The overall linguistic difficulty, reflected by Flesch Kincaid Grade level, was recorded by Bush(1989), whose address was suitable for the level of Grade 6 students. Our founding fathers have astonishing scores beyond 25 -- their inaugural addresses are understandable only by those well educated people. After that, the overall difficulty level kept decreasing until 1970s, after when it slowly increased. The overall difficulty of the new president's speech is at a similar level as Clinton(1997) and Bush(2001).

**SEMANTICS**

Besides the linguistic difficulty, I also investigated semantic similarity between all inaugural addresses. Two approaches were taken:

1. TF-IDF;
2. Latent Dirichlet Analysis(LDA).

Both are quite common models used to compare text similarity. A tricky part is in the text preprocessing step; as both models require identifying inflectional forms of the same word, lemmatizing or stemming is required. Stemming methods are readily available by Python's NLTK module, but stemming itself is a quite crude way of word processing. Therefore, I used lemmatizing by first applying Python's Stanford CoreNLP module to perform Part-Of-Speech(POS) tagging, before using NLTK module to lemmatize based on the POS tag.

For both models, I computed the cosine similarity between different inaugural addresses, and applied Local Linear Embedding to visualize. The results are the following:

![](https://dl.dropboxusercontent.com/u/72368739/blog/inaugural/lda_embed.png)
![](https://dl.dropboxusercontent.com/u/72368739/blog/inaugural/tfidf_embed.png)

LDA embedding seems not distinguish a lot among different presidents, perhaps because inaugural speeches are all about the same topics. TF-IDF describes more granular information, by looking at the common words used by different presidents. While presidents in the same era tended to use the same language, different political parties also spoke quite similarly. Caution that what politicians do are not what they say though.

**TECHNICAL DETAILS**

All technical details are included by my [codes](https://github.com/chandlerzuo/chandlerzuo.github.io/blob/master/codes/inaugural/inaugural.py).

*(c)2016-2025 CHANDLER ZUO ALL RIGHTS PRESERVED*

![](url)
