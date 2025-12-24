# Attention

## Overview

In this notebook, we develop the attention portion of an attention transformer using PyTorch.

## Theory

The objective of attention is to contextualize tokens based on previous tokens. To do so, each token has three key pieces of information in the form of vectors: a query, key, and value vector. A query vector pertains to the current token, and the key vector is relevant to the other tokens. By comparing the query vector to the key vectors, it determines how relevant the other tokens are to contextualizing the current token. The value vector is used to help update the embeddings once greater context is obtained. Each of these vectors is obtained by an associated weight matrix with the embedding for which the weights are learned from the model.

## Implementation

First, initialize the weight matrices and their biases with tensors of all ones and zeros. Note that there is also an output weight matrix that will be applied to obtain the final output.

A forward algorithm of the attention layer involves calculating the query, key, and value vectors. This is done by taking the dot products of the embeddings and the query, key, and value weight matrices using Einops' `einsum` and adding their associated biases.

Third, we calculate the dot products between the query and key vectors to get the attention score using `einsum`. Then, a causal mask is applied to create a lower triangular matrix, but with zeroes replaced with negative infinity so there is no data leakage from tokens after the current token. In other words, only previous tokens contribute to contextualization. Next, we convert the attention scores into probabilities by applying the softmax function over the key dimension. Softmax is why negative infinity is used instead of zero. With negative infinity, applying softmax outputs probabilities of zero.

Softmax is given by

$$Attention(Q,K,V)=softmax(\frac{QK^T}{\sqrt{d_k}})V$$

Fourth, we use `einsum` to take the weighted sum of the value vectors based on the attention probabilities to provide information on what to add to update the embeddings. 

Lastly, we use `einsum` to take the dot product of the output of the previous step with the output weight matrix, summing all the heads and adding the bias. The output is the updated embeddings.
