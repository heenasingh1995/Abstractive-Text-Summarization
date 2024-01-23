# Abstractive Text Summarization

## Introduction

In this modern era, data are getting generated day by day, and extracting the important information
from this huge amount of data has become a laborious and time-consuming task. So, to get the
important information from these lengthier documents we need text summarization. The job to
summarize a text document is to generate a short summary that consists of a few sentences and
captures the main idea of text document. Text summarization is a very important and interesting
problem in natural language understanding. It gives a precise summary so that humans can
understand the gist of long documents in less time.

### Types of Text Summarization
<p>
<b>1. Extractive Text Summarization</b> <br>
Extractive text summarization (ETS) is just extracting the important key-
words, phrases, sentences, and combining them to produce a summary<br>
Example : Heena went to NLP LAB. There, she setup her system.<br>
Extractive Summary : Heena went NLP LAB setup her system.<br>
In the above example, important words are selected and merged to generate the extractive
summary. <br><br>
<b>2. Abstractive Text Summarization</b> <br>
Abstractive text summarization (ABS) generates a more powerful summary
by generating new keywords, phrases, sentences and combine them to make a summary like humans
do. <br>
Example : Heena went to NLP LAB. There, she setup her system.<br>
Abstractive Summary : Heena visited NLP LAB to ready the system.<br>
In the above example, sentences are compressed and paraphrased to generate the abstractive
summary.
</p>

# Dataset Details & Analysis

<p>MSMO dataset has been used.
The size of the data is around 200 GB. <br>The structure of the text article file is shown in Figure below:</p>

<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/1f2a41cb-1faa-4d8d-abd7-f478aa7c2346.jpg" width="300" />


<p> Dataset Statistics are given below :<br></p>

|Data                   |  Number of Articles   | 
| -------------        | -------------         |  
|Training Data          |   293625              | 
|Validation Data        |   10339               | 
|Test Data              |   10245               | 

<br>
<b> Train, Validation, Test Documents Words count Distribution : </b>

<img src = "https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/ed512044-fa9c-4708-9989-e15ca3419991.png" width = "600" />

