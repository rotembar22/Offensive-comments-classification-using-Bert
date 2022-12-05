# Offensive-comments-classification-using-Bert


## Quick Links

  - [Overview](#overview)
  - [Dataset Description](#dataset-description)
  - [Chunking Approach](#chunking-approach)
  - [Bert Preprocess](#bert-preprocess)
  - [Bert Fine Tuning](#bert-fine-tuning)
  - [Model Results and Discussion](#model-results-and-discussion)  

# Overview

# Dataset Description

The data can be found here:
attack_annotated_comments.tsv: https://ndownloader.figshare.com/files/7554634
attack_annotations.tsv:        https://ndownloader.figshare.com/files/7554637

Comments:
<p align="center">
<img src="images/Screenshot 2022-12-05 125317.jpeg" width=50% height=50% >
</p>
We will use only the "comment" and the split features; comments contain the text we will process, and the split feature helps us split the data to train and test sets. Although we don't must split with the same portion, we can split by ourselves.

Annotations
<p align="center">
<img src="images/Screenshot 2022-12-05 125334.jpeg" width=50% height=50% >
</p>

Each comment can be reported as one of the following attacks: quoting_attack, recipient_attack, third_party_attack, and other_attack.
If one of them is positive (=1), the attack feature will also be positive. Therefore we will use only the attack feature. 
To label the comments, I defined an offensive comment when at least 50% of the reports were positive.

**Data distribution - Imbalanced data:**

13,590 comments are offensive
<br>102,274 comments are not 

This is highly imbalanced data. We need to e careful when choosing the right evaluation metric. Accuracy will be a bad metric. For example, a model that classifies all the instances as not offensive will get an accuracy of 88.27%. To evaluate our model, we will use AUC.

# Chunking Approach

The Bert model has an input limitation of the size of 512 tokens. Some of our comments exceed this limitation, and we need to address this issue. There are several approaches:

Taking the first 512 tokens
taking the last 512 tokens
Taking the first and the last of the tokens in the document. For example, taking the first 256 tokens and contacting them to the last 256 tokens.

I chose the first approach by taking the first X tokens.
Since Bert is a model that requires a lot of computer computing power, I took only the first 128 tokens. It will make the training much easier to train in terms of computing power.

# Bert Preprocess

Here are the preprocessing steps performed on the commets to prepare them for Bert model training:
* Pad comments that are in the size of less than 128 with '0' values.
* Create an attention mask indicate for the padded comments
* Add '[CLS]' to the beginning of a sentence and '[SEP]' at the end.
* Convert from NumPy to PyTorch tensors.


# Bert Fine Tuning

Bert is a word embedding model. So how will we use it in our classification problem?

The methodology will be as follow:
1. Encode the documents tokens-> we will get 128 vectors of the size 768
2. Perform document embedding by averaging the vectors from step 1. 
3. Feed the vector to a classification model

<br>In this project, I decided to use BertForSequenceClassification.
BertForSequenceClassification is a BERT model with an added single linear layer on top for classification that we will use as a sentence classifier. The entire pre-trained BERT model and the additional untrained classification layer are trained on our specific task as we feed input data.
