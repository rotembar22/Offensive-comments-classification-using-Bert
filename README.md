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
102,274 comments are not 

This is highly imbalanced data. We need to e careful when choosing the right evaluation metric. Accuracy will be a bad metric. For example, a model that classifies all the instances as not offensive will get an accuracy of 88.27%. To evaluate our model, we will use AUC.

# Chunking Approach

