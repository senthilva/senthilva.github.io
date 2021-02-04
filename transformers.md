# Understanding the transformer

This blog is to document my understanding of the transformer paper [**Attention is all you need**](https://arxiv.org/pdf/1706.03762.pdf)

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
  - Attention : is calculated as a **softmax** (**Q** * **K**) * **V** . The intuition is to use similarity/dependency using **Q** * **V** and use softmax to build attention over all words in the input. This in essence helps build context factoring all words in the input.
- The above is done independently 8 times hence the **multi headed** self attention. These 8 values are weighted again to give the final attention
- The self attention output is added with the skip connections of the input and normalized.
- This then passes through a fast forward neural network. 
- The above in essence the heart of the encoder. 
 
 This is repeated **N**times based on how the network is designed. The final output is then sent to the decoder.
   
  


## Decoder

Works very similar to encoder with some key differences

- Each word is decoded one word at a time
- Each of the word is converted to its corresponding embedding + positional encoding 
- As the decoder need to build attention only on the words before it during self attention - words after are masked 
- **self attention** 
  - Queries **Q** : each incoming germna embedding is treated as a query.  
  - Keys **K** : for self attention keys are also the german word embeddings
  - Values **V** : for self attention keys are also the german word embeddings
- The self attention output is added with the skip connections of the input and normalized.
- **attention with encoder** 
  - Queries **Q** : each incoming germna embedding is treated as a query.  
  - Keys **K** : **here the keys are encoder ouputs**
  - Values **V** : **here the keys are encoder ouputs**
- The above is added with the skip connections and normalized.
- This then passes through a fast forward neural network. 
- The above in essence the heart of the decoder. 

This is repeated **N**times based on how the network is designed. The final output is then sent to fully connected network and softmax for predicting the probable german word !

## Training

The gold data is used to calculate the loss of the final decoder which is then used in back propogation to train the decoder and encoder.



