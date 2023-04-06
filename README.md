# Chatbot-using-GRU-with-Attention
 
### Dataset:  

 Cornell Movie Dialogs corpus contains a large metadata-rich collection of fictional conversations extracted from raw movie scripts.
 The corpus includes:
- 220,579 conversational exchanges between 10,292 pairs of movie characters
- involves 9,035 characters from 617 movies
- in total 304,713 utterances

I have used only 96048 pairs of these dialogs.

A conversation example from the dataset:

```
Can we make this quick?  Roxanne Korrine and Andrew Barrett are having an incredibly horrendous public break- up on the quad.  Again.
Well, I thought we'd start with pronunciation, if that's okay with you.

Well, I thought we'd start with pronunciation, if that's okay with you.
Not the hacking and gagging and spitting part.  Please.

Not the hacking and gagging and spitting part.  Please.
Okay... then how 'bout we try out some French cuisine.  Saturday?  Night?

You're asking me out.  That's so cute. What's your name again?
Forget it.

No, no, it's my fault -- we didn't have a proper introduction ---
Cameron.
```

### Model:

I utilized Encoder-Decoder architecture for the task. The encoder is a 1-layer Bi-directional GRU with 256 units and the decoder is a 2-layer Uni-directional GRU with 512 units. I adopted Bahdanau Attention mechanism as my attention model.

![image](https://user-images.githubusercontent.com/61462986/230452719-1e529124-73fb-446e-91b6-75d81487e224.png)

### Results:

You can observe how the model decided to generate the output based on the input. For each pair of words from input and output the attention weight is visualized.

![image](https://user-images.githubusercontent.com/61462986/230452855-658523f6-78db-4515-98e5-24daf8afe5b9.png)


### Tips for training the model:

* I used small batch size of 32 for more stable training.
* I used bidirectional GRU as the encoder, but decoder is unidirectional. It is due to the fact that input is known but output is generated at each step.
* I used Masked Loss. The loss for the padding inputs are considered 0.
* With a simple model like the one I have used, It is more desirable to use a low dimension word Embeddings. I used 50-d GloVe word vectors.
* I applied dropout with a chance of 0.2 to encoder's input word embeddings.
* Instead of feeding a whole sequence to the network, I have fed time step x of a batch of data to the network, as depicted below:

![image](https://user-images.githubusercontent.com/61462986/230452903-d7adc6ed-d7cd-445f-80b8-c15aa90636fa.png)

### Setup:

* I trained the model on a Nvidia 1070-Ti GPU. Each epoch took about 4 minutes. I used the 120th epoch for the inference.

### Helpful tutorials:

* https://homes.cs.washington.edu/~msap/notes/seq2seq-tricks.html
* https://machinelearningmastery.com/configure-encoder-decoder-model-neural-machine-translation/
* https://pytorch.org/tutorials/beginner/chatbot_tutorial.html
* https://www.tensorflow.org/tutorials/text/nmt_with_attention

