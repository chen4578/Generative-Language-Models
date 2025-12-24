# Stochastic Decoding

## Overview

In this project, we develop three different stochastic decoding methods: top-k, top-p, and temperature sampling to generate text given the logits.

## Dataset

For the purposes of this notebook, a pretrained GPT-2 model is used. No dataset was loaded in the notebook.

## Implementation

### Top-K Sampling

PyTorch has the `topk` function, which returns the `k` greatest items of a tensor along a specific dimension. Specifically, our inputs are the logits tensor and the k largest logits that we want to consider. By using `.indices()', we obtain the indices of the k largest logits. Afterwards, mask the other indices with negative infinity.

The sampling portion involves applying softmax and appending the token selected using `torch.multinomial`.

A greedy search is a special case of top-k sampling where k = 1.

### Top-P Sampling

PyTorch does not have a top-p sampling function, so we code one from scratch. 

Start by calculating the probabilities and sorting them in descending order. Then, calculate the cumulative probabilities. Keep the smallest set of tokens that have a cumulative sum greater than p and mask the rest with negative infinity.

As with top-k sampling, apply softmax and choose a token with `torch.multinomial`.

### Temperature Sampling

Temperature sampling is simply dividing the logits by temperature, applying softmax, and sampling using `torch.multinomial`.

When the temperature is extremely large, each token has about equal probability. There is a high chance of gibberish emerging. When the temperature is greater than 1 but not extremely large, the probabilities are closer together. It is more "creative" but also more error-prone. When the temperature is close to 1, the logits are nearly unscaled. When the temperature is between 0 and 1, the high probabilities are magnified while low probabilities are miniaturized, leading to greater selection of high-probability tokens but with less rigidity compared to greedy search. As the temperature approaches 0, temperature sampling appears more like a greedy search.

## Results

The following are sample outputs comparing greedy search, top-k, top-p, and temperature sampling.

Greedy: Once upon a time, there was a man who was a man of great wealth and power. He was a man of great wealth and power. He was a man of great wealth and power. He was a man of great wealth and power

Top-k: Once upon a time, there was a great deal to do. The people of the land had a strong desire to do good. The people of this country were not satisfied with their present situation, and so the government decided that they should do

Top-p: Once upon a time, there was a vastly increasing number of large oceanic changes of arrangement that please captivate the inhabitants of the Grand Continental, few regard the Pacific ones as more relative to their ecological purposes than the Pacific Ocean.

Temperature: Once upon a time, there was a friction between river names, great lords phinet seniors concocting wines connected life national problem holes multiplied problem scheme, change from powerful art budget wizard to stellar directors ancestors contacting Heaven champ Bob Bowman Apollo Creed extrater

We also attempted to combine temperature sampling with top-k and top-p sampling to obtain the following sample outputs:

Temperature and Top-k: Once upon a time, there was a new light for mankind—the day would never stop." [Emir Karrass's "Inherent Vibrantes," volume one]. As if we would no end. There could also lie to

Temperature and Top-p: Once upon a time, there was a call feeling to Bird urging because, per approach comedances, Goodaine does horror Teg plenty by infusing took place before Die
