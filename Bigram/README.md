# Bigram Model

## Overview

In this project, we develop a bigram model for text prediction using PyTorch. Specifically, this model predicts the successive character based on the current character.

## Dataset

The dataset used in the project comes from Project Gutenberg's collection of Shakespeare's sonnets: https://www.gutenberg.org/files/1041/1041-0.txt. Data is batched and shuffled.

## Implementation

The bigram model consists of two major layers: an embedding layer that converts tokens to vectors and a prediction layer that predicts the next token.

### Embedding Layer

The first part of the embedding stage is to tokenize the input text. The possible tokens in consideration consist of the uppercase and lowercase letters, as well as a select number of punctuation marks. Next, the tokens are one-hot encoded as vectors. Finally, a linear projection is applied to the vectors.

### Neural Network

The output of the embedding layer is passed through two fully connected linear layers with ReLU activation functions. Cross-entropy loss is the loss function, and gradient descent is performed using the AdamW optimizer. The output layer outputs the logits. Detokenizing the output by obtaining the highest value in the tensor allows us to identify the predicted character.

## Results

With an input of "Shall I compare thee to a summer's day?" The following predictions are simply repetitions of the word "the." However, this is expected of the character-by-character prediction performed by this bigram model, where it predicts the word with the most occurrences in the data. Future models will tackle such issues.
