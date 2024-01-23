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


# Results & Analysis
<p>
We have evaluated our generated summary on BLEU score and ROUGE score.
 </p>
 
<b> BLEU Score Results :</b>
 
<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/8345dc3c-057a-4e01-ac68-ccf4ec0e746f.jpg" width="600" />


 
<b> ROUGE Score Results :</b>
 
 
<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/25c1c4de-7083-4b39-8844-cd2e4c13d92c.jpg" width="600" />
<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/63b70b30-a266-4f35-8590-50964933c4a4.jpg" width="600" />


## Comparative Analysis

<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/b9da3e4a-8a3a-4725-a74b-9ee5db2b17b6.jpg" width="600" />


## Output Summary Examples

<img src="https://github.com/heenasingh1995/Abstractive-Text-Summarization/assets/47137754/b1a59e3d-67c1-40ab-bd72-1630a317f2bb.jpg" width="600" />


# Publications

<p>

Kumari H., Sarkar S., Rajput V., Roy A. (2020) <b>Comparative Analysis of Neural Models for Abstractive Text Summarization</b>. <br> In: Bhattacharjee A., Borgohain S., Soni B., Verma G., Gao XZ. (eds) Machine Learning, Image Processing, Network Security and Data Sciences. MIND 2020. Communications in Computer and Information Science, vol 1241. Springer, Singapore. <br> https://doi.org/10.1007/978-981-15-6318-8_30

</p>

# References
<p>

[1] Bahdanau, D., Cho, K., Bengio, Y.: Neural machine translation by jointly learning to align
and translate. In: Bengio, Y., LeCun, Y. (eds.) 3rd International Conference on Learning Rep-
resentations, ICLR 2015, San Diego, CA, USA, May 7-9, 2015, Conference Track Proceedings
(2015), http://arxiv.org/abs/1409.0473 <br>
[2] Cho, K., van Merriënboer, B., Bahdanau, D., Bengio, Y.: On the properties of neural ma-
chine translation: Encoder–decoder approaches. In: Proceedings of SSST-8, Eighth Workshop
on Syntax, Semantics and Structure in Statistical Translation. pp. 103–111. Association for
Computational Linguistics, Doha, Qatar (Oct 2014). https://doi.org/10.3115/v1/W14-4012,
https://www.aclweb.org/anthology/W14-4012 <br>
[3] Gehring, J., Auli, M., Grangier, D., Yarats, D., Dauphin, Y.N.: Convolutional sequence to
sequence learning. CoRR abs/1705.03122 (2017), http://arxiv.org/abs/1705.03122 <br>
[4] Gulcehre, C., Ahn, S., Nallapati, R., Zhou, B., Bengio, Y.:
words. In:
Pointing the unknown
Proceedings of the 54th Annual Meeting of the Association for Compu-
tational Linguistics (Volume 1:
Long Papers). pp. 140–149. Association for Computa-
tional Linguistics, Berlin, Germany (Aug 2016). https://doi.org/10.18653/v1/P16-1014,
https://www.aclweb.org/anthology/P16-1014 <br>
[5] Guo,H.,Pasunuru,R.,
tionwithentailmentand
Bansal,
M.:
question
Soft layer-specific multi-task summariza-
generation.
CoRR
abs/1805.11004
(2018),
http://arxiv.org/abs/1805.11004 <br>
[6] Jaya Kumar, Y., Goh, O.S., Basiron, H., Ngo, H.C., Suppiah, P.: A review on automatic text
summarization approaches 12, 178–190 (01 2016). https://doi.org/10.3844/jcssp.2016.178.190 <br>
[7] Klein, G., Kim, Y., Deng, Y., Nguyen, V., Senellart, J., Rush, A.: OpenNMT: Neu-
ral machine translation toolkit. In: Proceedings of the 13th Conference of the Associ-
ation for Machine Translation in the Americas (Volume 1: Research Papers). pp. 177–
184. Association for Machine Translation in the Americas, Boston, MA (Mar 2018),
https://www.aclweb.org/anthology/W18-1817 <br>
[8] Lin, C.Y.: ROUGE: A package for automatic evaluation of summaries. In: Text Summariza-
tion Branches Out. pp. 74–81. Association for Computational Linguistics, Barcelona, Spain
(Jul 2004), https://www.aclweb.org/anthology/W04-1013 <br>

[9] Miao, Y., Blunsom, P.:
Language as a latent variable:
els for sentence compression. In:
Discrete generative mod-
Proceedings of the 2016 Conference on Empiri-
cal Methods in Natural Language Processing. pp. 319–328. Association for Compu-
tational Linguistics, Austin, Texas (Nov 2016). https://doi.org/10.18653/v1/D16-1031,
https://www.aclweb.org/anthology/D16-1031 <br>
[10] Papineni, K., Roukos, S., Ward, T., Zhu, W.J.: Bleu: a method for automatic evalua-
tion of machine translation. In: Proceedings of the 40th Annual Meeting of the Associ-
ation for Computational Linguistics. pp. 311–318. Association for Computational Linguis-
tics, Philadelphia, Pennsylvania, USA (Jul 2002). https://doi.org/10.3115/1073083.1073135,
https://www.aclweb.org/anthology/P02-1040 <br>
[11] Rush,
A.M.,
Chopra,
S.,
Weston,
tive sentence summarization. In:
J.:
A neural attention model for abstrac-
Proceedings of the 2015 Conference on Empiri-
cal Methods in Natural Language Processing. pp. 379–389. Association for Computa-
tional Linguistics, Lisbon, Portugal (Sep 2015). https://doi.org/10.18653/v1/D15-1044,
https://www.aclweb.org/anthology/D15-1044 <br>
[12] See, A., Liu, P.J., Manning, C.D.: Get to the point: Summarization with pointer-generator
networks. In: Proceedings of the 55th Annual Meeting of the Association for Compu-
tational Linguistics (Volume 1: Long Papers). pp. 1073–1083. Association for Computa-
tional Linguistics, Vancouver, Canada (Jul 2017). https://doi.org/10.18653/v1/P17-1099,
https://www.aclweb.org/anthology/P17-1099 <br>
[13] Song,S.,
inglstm-cnn
tions
Huang,
78(1),
H.,
based
Ruan,
deep
857–875
T.:
learning.
(2019).
Abstractive
Multimedia
text
summarization
Tools
and
us-
Applica-
https://doi.org/10.1007/s11042-018-5749-3,
https://doi.org/10.1007/s11042-018-5749-3 <br>
[14] Sutskever, I., Vinyals, O., Le, Q.V.: Sequence to sequence learning with neural networks. In:
Ghahramani, Z., Welling, M., Cortes, C., Lawrence, N.D., Weinberger, K.Q. (eds.) Advances
in Neural Information Processing Systems 27, pp. 3104–3112. Curran Associates, Inc. (2014),
http://papers.nips.cc/paper/5346-sequence-to-sequence-learning-with-neural-networks.pdf <br>
[15] Zhu, J., Li, H., Liu, T., Zhou, Y., Zhang, J., Zong, C.:
MSMO: Multimodal sum-
marization with multimodal output. In: Proceedings of the 2018 Conference on Empir-
ical Methods in Natural Language Processing. pp. 4154–4164. Association for Computa-
tional Linguistics, Brussels, Belgium (Oct-Nov 2018). https://doi.org/10.18653/v1/D18-1448,
https://www.aclweb.org/anthology/D18-1448 <br>
</p>
