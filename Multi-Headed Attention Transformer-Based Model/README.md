# Multi-Headed Attention Transformer-Based Model

## Overview

In this project, we aim to create a multi-headed attention transformer-based model for text generation using PyTorch.

## Dataset

The dataset used in the project comes from a selection of Shakespeare's works: https://raw.githubusercontent.com/karpathy/char-rnn/master/data/tinyshakespeare/input.txt.

## Implementation

Our transformer will be implemented using several modules: layernorm, a head of self-attention, multiple heads of self-attention, a transformer block, and the model.

### Modules

#### LayerNorm

LayerNorm normalizes the inputs so that the mean is 0 and the variance is 1. This is a z-score normalization. LayerNorm extends this so that the distribution is able to be scaled and shifted. Formally, LayerNorm can be written as

$$
y=
\boldsymbol{\gamma} *
\frac{\mathbf{x} - \mu}{\sqrt{\sigma^2 + \epsilon}}
+
\boldsymbol{\beta}
$$

where the input is x, the mean is $$\mu$$, and the standard deviation is $$\sigma$$. The scaling and shifting parameters are $$\gamma$$ and $$\beta$$, respectively. Finally, \epsilon is a small value added to prevent divisions by zero.

Since $$\gamma$$ and $$\beta$$ are tunable parameters, they are initialized with PyTorch's `nn.Parameter`.

#### Head of Self-Attention 

A head of self-attention was implemented in the Attention.ipynb notebook, and the README provides a thorough description of its implementation. The implementation is similar but not identical. A more brief summary will be provided for this module.

First, initialize the key, query, and value vectors and their weights using PyTorch's `nn.Linear`. Then, we calculate the dot products between the query and key vectors to get the attention score. Then, applied a causal mask. Next, use softmax to get the attention probabilities. Perform dropout to reduce overfitting. Afterwards, get the weighted sum of the value vectors based on the attention probabilities to acquire the output.

#### Multi-Headed Attention 

This module feeds the inputs through all the attention heads in parallel and concatenates their outputs along the embedding dimension.

#### Transformer Block 

The transformer block passes the input through the multi-headed attention and LayerNorm layer and adds the output to the input to update the input. There is no feedforward network.

#### Model

Start by initializing the token and position embedding tables, a sequential stack of the transformer blocks, the LayerNorm layer, and the projection layer.

A pass through the model involves creating and adding the embeddings, passing through the attention layers, applying LayerNorm, and obtaining the logits using the linear layer. Next, the logits are flattened and the cross-entropy loss is calculated.

### Training

After initializing and putting the input and target through the model, repeatedly calculate the loss, optimize using AdamW, and perform backpropagation. Note that evaluation happens at specific intervals, not necessarily every epoch.

### Text Generation

The generation consists of applying softmax to the final logits, sampling using `torch.multinomial` (in the past, `argmax` was used, which was a greedy algorithm), and appending. Lastly, we decode the concatenated sequence.

## Results

The following is sample text outputted by the model:

I hour ill hath love owself
The parking there and thy son my aimsly to gracge:
I have his wear not reoth. Botcen-a guit?

NoULIA:
I'll be and thust you, all gues?

ISTEOLNTIO:
I fat sanUS:
Which thight of ownd the proptokend the liss no is shon!

CBULENIZESTEY:
He hill grava alt daughfast the of Yurthus.

CYORPOMNRO:
Thore, sir:
Neath, bettem temper. O, York,
Thow do dy have on the crance and to that look.
How patortizencate acle! I this sive; iny.

ISIC:
It 'ForwiS:
Ark ques the prose.

Now My RETFFFARD, I:
My you with blo;
O shour meen your make confurt
This tenche of her shamer to lowble yiex's!

Now FOrcunwer all
The the dost art I for my lland kithily the all be
Faht phread, prenty a with it to PourTine if be is is plust tendrlight
To for abouns badk ussead, fhow I cave upet where of A
Thor'd thought on yet to perty blift,
I as bruchs mank know
Pliploter,-dis mee youn's. Now there will thes do,
Whas? who pedce, of Once, angfirepons
Forse upon an breap'Twarrs, what.

FIRIA:
O their rave I babount
That haven out is and sewsear exteo his that don alived bad.

DUKES:
Aisbd; bescara joot of joy no for this new hell comsand:
I past hate kings to palter his agaiseer ailough balt one,
I'ent would 'ret signingh;
Antal brother entes yours, mercomme;
Ditor to preant. Who did yet time light.
I, by it, forslasge say, woyed.

ISABELLA:
Atill, where it rover their pray, be
The house this hescious solot us heaves
Work know, oath's a by land besfes! I softrriise, and do feer at gilser is heres?

HERMVOLO:
Nedion womb thid to taste your hortorthy,
Your prim t
My me all best-'s for I nUwasty,
'd with to Kanccy end!' montgong
Nor his you fikcity peave a taitied More:
May moly for my tho worth will, and lokn.

LORTOMNERNA:
O Come here the pacge thought--ramang to Edvop yound at tive this.

MONIUS:
LICESTINI:
No, thought of Lowird ling shing, in fladst truke! The his by blook
Polown: I nat som woman: I his fasaurperishal.
