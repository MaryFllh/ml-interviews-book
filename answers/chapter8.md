1. RNNS
    1. [E] What’s the motivation for RNN?
        The motivation behind Recurrent Neural Networks is to capture the dependencies of the observations in a sequence of data, e.g. time series or natural language. For instance, in natural language the words in a sentence are not independent of one another and knowing the first three words can help you guess the forth word. RNNs aim to capture this dependency by passing the information from the previous inputs when processing the current input.
    1. [E] What’s the motivation for LSTM?
        RNNs have the issue of long-term dependencies due to vanishing gradients, LSTMs (and GRUs) were introduced to overcome this issue by allowing information from early layers directly to later layers. The forget gates in LSTMs structure allows for the network to selectively remember/forget information from time step to the next.
    1. [M] How would you do dropouts in an RNN?
        Dropout can be applied in a RNN in different ways:

        1. It can be applied to the hidden state that goes to the output and not to the next timestamp. Note that different samples in a mini-batch should have different dropout masks but the same sample in different time steps should have the same mask
        2. It can be applied to the inputs x_t
        3. It can be applied to the weights between the hidden states. Note that the same dropout mask should be used for all time steps in a mini-batch
2. [E] What’s density estimation? Why do we say a language model is a density estimator?
    Density estimation means estimating the probability density function (PDF) of a random variable from a set of observations. The PDF of a variable describes the probability of the variable taking on different values. 

    Language models are trained on sequences of words to learn the probability of words occurring. In other words, they are estimating the PDF of word sequences and can therefore be interpreted as density estimators.
3. [M] Language models are often referred to as unsupervised learning, but some say its mechanism isn’t that different from supervised learning. What are your thoughts?
    Language models are trained on vast amounts of text without any explicit labels. In that regard they are unsupervised. But in order for the model to learn the intricacies of the language, the relationship between different words it is usually trained in an auto-regressive manner, i.e. a set of words are masked and the model is trained to predict the masked words. These masked words can be thought of as labels which is similar to supervised learning.
4. Word embeddings.
    
    1. [M] Why do we need word embeddings?
    
    Word embeddings are a way to map words to vector representations that can be used in matrix multiplication in neural networks. These representations preserve the semantics and are lower in dimension than one-hot encoded vectors.
    
    2. [M] What’s the difference between count-based and prediction-based word embeddings?
    
    Count-based embeddings learn the embeddings based on the co-occurrences of words across a large dataset. GloVe is a count-based embedding method. Prediction-based word embeddings learns the embeddings by learning to predict a word of set of words based on the surrounding words and minimising the prediction loss
    
    3. [H] Most word embedding algorithms are based on the assumption that words that appear in similar contexts have similar meanings. What are some of the problems with context-based word embeddings?
    
    Context-based embeddings reinforce gender and racial biases present in the training data. For example the embedding of the word smart or beautiful should not have any gender preferences baked into it but if you ask a LM to describe someone smart or translate a sentence describing someone smart from a gender-neutral language to English for instance, it will prefer the pronoun he for smart and she for beautiful because in the context of other words in the training data smart is more associated with males and beauty with females. 
    
    Another issue can be that words with different meaning will have different embeddings which make it difficult for them to be used standalone.

10. [M] BLEU is a popular metric for machine translation. What are the pros and cons of BLEU?

    Pros:

    1. It is widely used so different models can be compared with one another
    2. It is easy to implement. It only needs the target and prediction to calculate the precision for different n-grams

    Cons:

    1. Does not consider semantics and only relies on same tokens this has two issues: it penalises translations that convey the same meaning but use different words. On the other hand, it doesn’t penalise translations that are semantically incorrect but have a lot of overlapping words