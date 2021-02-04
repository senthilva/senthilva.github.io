# Understanding the transformer

This blog is to walk through the transformer paper [**Attention is all you need**](https://arxiv.org/pdf/1706.03762.pdf)

We will walkthrough the encoder and decoder for translating from English to German.

## Encoder

Let us consider an English sentence : " The weather is good" . The following steps are followed in the encoder

- Each of the word is converted to its corresponding embedding 
- The above embedding is added with the positional embedding => As RNNs are not used , there needs to be a way to encode the positions
- To understand contextual information **multi-headed self attention** is used
- **self attention** 
  - Queries **Q** : each resultant word embedding is treated as a query.  
  - Keys **K** : as in the encoder we are calculating self attention within the source sentence - keys are also the source word embeddings
  - Values **V** : as in the encoder each resultant word embedding is treated as a values too.
  - Attention : is calculated as a **softmax** (**Q** * **K**) * **V** . The intuition is to use similarity/dependency using **Q** * **V** and use softmax to build attention over all words in the sentence. ** This in essence helps build context factoring all words in the input.
  - The above is done independently 8 times hence the **multi headed** self attention. These 8 values are weighted again to give the final attention
   
  


## Decoder

## Training



