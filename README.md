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

<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/1f2a41cb-1faa-4d8d-abd7-f478aa7c2346.jpg" width="500" />


<p> Dataset Statistics are given below :<br></p>

|Data                   |  Number of Articles   | 
| -------------        | -------------         |  
|Training Data          |   293760              |
|Validation Data        |   10344               | 
|Test Data              |   10251               | 

<br>
<b> Train, Validation, Test Documents Words count Distribution : </b>

<img src = "https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/ed512044-fa9c-4708-9989-e15ca3419991.png" width = "600" />


# System Architecture
To generate abstractive text summary, there models have been used.

<b>1. Encoder - Decoder with Attention Mechanism :</b> <br>
Encoder-Decoder with attention model was introduced by Bahdanau for machine translation and is depicted in Figure below. Later it has been used by many researchers as a baseline system for their research work. In this encoder-decoder model, encoder compress input sequence W = (w1 , w2 , ......, wTx ) to a fixed-length vector. The decoder produces output at each timestamp. The encoder will produce hidden state  by taking word and previous hidden state  in every time step. The output of the last timestamp of the encoder is given to the decoder as initial input. At each timestamp t, the decoder will predict a target word by a soft search for the relevant part of the source sentence.


<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/16eb4354-0398-44ea-a0fe-f44989a7def0.jpg" width="400" />
<br>

<b>2. Pointer Generator Network :</b> <br>

The previous model has several disadvantages. It reproduces factual details inaccurately and
cannot output the of words which are absent in vocabulary and also repeat themselves. This can
be overcome by PGN [12]. PGN can extract words from the input article through pointing, that
produces the correct factual details, while novel words will be produced through the generator.
This network can be called a combination of extractive and abstractive text summarization. The
context vector is the same as in the previous model and attention distribution also.

<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/fbf4a28a-d504-49c2-bcce-80e9f05eba97.jpg" width="600" />
<br>
<br>

<b>3. Pointer Generator Network with Coverage Mechanism :</b> <br>

There is a problem of the repetition of words in our previous seq2seq models. So, there is a need for something to keep track of what has been summarized so that the repetition of words can be controlled in the generated summary. So coverage mechanism is used to track what is already summarized. It prevents the repetition of words.
<br>

# Experiment

### Data Pre-Processing
<p>
The following steps have been done to pre-process the text data:<br>
1. Converted the text into lower case. <br>
2. Contractions have been expanded. Ex. can’t to cannot.<br>
3. Removed special characters and symbols like ’,?/+=)( and numeric values also.<br>
4. Truncated the source article after 100 words and target summary after 25 words.<br>
An example of a text article before pre-processing and after pre-processing is shown in table 5.1.<br>
</p>

<img src="https://user-images.githubusercontent.com/26309477/120082771-6683fd00-c0e2-11eb-8101-afb06c261d4f.jpg" width="500" />

<img src="https://user-images.githubusercontent.com/26309477/120082776-6ab01a80-c0e2-11eb-81a2-d186c3366984.jpg" width="500" />

### Creating Vocabulary
<p>
There are a total of 234682 unique words in source training articles. Only the top 230000 most
frequent words are taken in the source vocabulary. Including start and end token, the total source vocab size is 230002.

There are a total of 88631 unique words in the target training summary. Only the top 85000
most frequent words are taken for the target vocabulary. Including start and end token, the
total target vocab size is 85004.
</p>
 
 <img src="https://user-images.githubusercontent.com/26309477/120082861-f45fe800-c0e2-11eb-8f9c-17130b59ec86.png" width="600" />
