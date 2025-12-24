# Generative Language Models

This repository contains the Colab Notebooks I completed in the ACM AI, a subbranch of UCLA's student chapter of the Association for Computing Machinery (ACM). Specifically, these projects were a part of ACM AI's projects track, which covered text generation models such as bigram, attention, transformer, and stochastic decoding models.

## Project Overviews

### Bigram Model

This project involves text generation where each token was a single character and the model predicts the next character based only on the current character. The model consists of a tokenization and embedding layer followed by a fully connected neural network.

The results of this simple model often result in the word "the" appearing repeatedly. Later models will be more robust.

### Attention

This notebook was an introduction to attention. In the code, query, key, and value vectors were calculated along with the associated weight matrices. Furthermore, the code demonstrates how embeddings can be updated through attention. No text was generated in this notebook.

### Multi-Headed Attention Transformer-Based Model

For this model, we implemented heads of self-attention and fed the inputs into multiple heads in parallel to perform multi-headed attention. The model also had a transformer block that passes the input through the multi-headed attention and LayerNorm layer and updates the input. Note that this is not a full transformer because there is no feedforward network. 

The model passes the embeddings through the attention layers, the LayerNorm layer, and a linear layer to acquire the logits.

Training is performed using a neural network with AdamW. The tokens were selected by sampling from a probability distribution.

Here is a snippet of one output: 

I hour ill hath love owself The parking there and thy son my aimsly to gracge: I have his wear not reoth. Botcen-a guit?

NoULIA: I'll be and thust you, all gues?

ISTEOLNTIO: I fat sanUS: Which thight of ownd the proptokend the liss no is shon!

### Stochastic Decoding

This project implements top-k, top-p, and temperature sampling and compares these methods with greedy search. Temperature sampling was also combined with top-k and top-p sampling.

The following is a snippet of the results:

Greedy: Once upon a time, there was a man who was a man of great wealth and power.

Top-k: Once upon a time, there was a great deal to do. The people of the land had a strong desire to do good. 

Top-p: Once upon a time, there was a vastly increasing number of large oceanic changes of arrangement that please captivate the inhabitants of the Grand Continental, few regard the Pacific ones as more relative to their ecological purposes than the Pacific Ocean.

Temperature: Once upon a time, there was a friction between river names, great lords phinet seniors concocting wines connected life national problem holes multiplied problem scheme

Temperature and Top-k: Once upon a time, there was a new light for mankind—the day would never stop.

Temperature and Top-p: Once upon a time, there was a call feeling to Bird urging because, per approach comedances
