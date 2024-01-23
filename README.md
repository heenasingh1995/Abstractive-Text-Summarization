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

## Data Pre-Processing
<p>
The following steps have been done to pre-process the text data:<br>
1. Converted the text into lower case. <br>
2. Contractions have been expanded. Ex. can’t to cannot.<br>
3. Removed special characters and symbols like ’,?/+=)( and numeric values also.<br>
4. Truncated the source article after 100 words and target summary after 25 words.<br>
An example of a text article before pre-processing and after pre-processing is shown below.<br>
</p>

<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/24aff1f5-d7f2-4e03-a566-1d14ce259df1.jpg" width="500" />


## Creating Vocabulary
<p>
For source vocabulary, only 210000 and for target vocabulary, only 80000 highest frequency words
were taken. After adding the start and end token, the source vocabulary size was 210002 and the
target vocabulary size was 80004. 50 highest frequency words in source and target vocabulary are
shown in figure
</p>

<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/8edb8ac3-7916-4948-880c-49ab6bc6f7d5.jpg" width="600" />

<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/bace165c-a6db-4cab-b0e2-22ae666d953f.jpg" width="600" />

## Training

<p>
In all the three experiments, a bi-directional LSTM is used as an Encoder which outputs a 512-
dimensional hidden state with a dropout rate 0.3 and an LSTM Decoder which outputs a hidden
state of 512-dimensions with a dropout rate 0.3. Also for all the experiments, the source vocabulary
is of 210002 words and the target vocabulary is of 80004 words. Also, each word is embedded in
128 dimensions. Each model’s validation accuracy was checked for every 1000 epochs. For all the
experiments, a batch size of 128 and adagrad optimizer with a learning rate of 0.15 are used.
In the first experiment, Bahadanu’s attention mechanism is used. There are a total of
82366852 training weights. The model was trained for 50000 epochs. Validation accuracy was
35.1372 at 50000 epochs. It took around 4 hours to train the model.
In the second experiment, the Pointer Generator network is used. There are a total of 83417477
training weights. With pointer generator network 1050625 more training weights were added as
compared to the first experiment. The model was trained for 40000 epochs. The validation accuracy
was 37.9021 at 40000 epochs. Model training took around 7.5 hours.
In the third experiment, we have used a coverage mechanism with the pointer generator network.
There are a total of 83417989 training weights. In this experiment, 512 more training weights were
added as compared to the second experiment. The model was trained for 40000 epochs. Validation
accuracy as 37.8786 at 40000 epochs. Model training took around 9 hours.
Each model’s training loss, training accuracy and validation accuracy is shown by graph in
figure 5.3, 5.4 and 5.5 respectively.

</p>


<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/77476a2b-ba84-47c0-a017-a510f2fe7358.jpg" width="600" />

<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/6f0e15dc-d1b4-4c5a-ad7f-0e56ab93bcb2.jpg" width="600" />

<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/03185288-f854-4d97-b810-389e087290ef.jpg" width="600" />


