# Offensive-comments-classification-using-Bert


## Quick Links

  - [Overview](#overview)
  - [Dataset Description](#dataset-description)
  - [Chunking approach](#chunking-approach)
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

