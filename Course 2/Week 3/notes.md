# N-Grams and Probabilities

## N-Gram
<p>An N-Gram is essentially a sequence of N words. Unigrams are N-Grams where the value of N is equal to 1, bigrams are N-grams where the value of N is equal to 2, and so on.</p>

![N Gram](images/image1.png)

## Sequence Notation

<p>We can use the notation shown below where the subscript denotes the starting word and the superscript denotes the last word.</p>

![Notation](images/image2.png)

## Bigram Probability

<p>To calculate the probability of occurence of a bigram, we can use conditional probability where we divide the number of occurences of the bigram by the number of occurences of the first word in the bigram.</p>

![Bigram Prob](images/image3.png)

## Trigram Probability

<p>To calculate the probability of occurence of a trigram, we can use conditional probability where we divide the number of occurences of the trigram by the number of occurences of the first two words in the trigram.</p>

## N-Gram Probability

<p>We can generalize our approach and find the probability of N-grams by dividing the number of occurences of the N-grams by the number of occurences of the first N-1 words of the N-gram.</p>

![N-Gram](images/image4.png)

# Sequence Probabilities

## Probability of a sequence

<p>We can use conditional probability and the chain rule to find the probability of a sequence. This can be intuitively understood as the product of all conditional probabilities for a word conditioned the earlier words in the sequence occur.</p>

![Probability of a Sequence](images/image5.png)

<p>The problem with this approach is that it is difficult to find such exact sequences in the corpus and hence the probability generally tends to 0.</p>

![Problem](images/image6.png)

## Approximation of Sequence Probability

<p>To avoid this problem, we can approximate values to conditions extending only to the immediately previous word.</p>

![Approx](images/image7.png)

<p>This is a Markov Assumption where we assume that the current state depends only on the previous state. We can extend this by considering N previous words instead of one.</p>

![Extension](images/image8.png)

# Starting and Ending Sentences

<p>For us to consider a window of N-words to calculate sequence probabilities, we need to insert N-1 start tokens at the start of the sentence in order to calculate the conditional probability of the first N-1 words.</p>

![Start](images/image9.png)

<p>However, the problem with this approach is that it fails to consider sequences of different lengths in the probability calculation and we can use end tokens to solve this problem.</p>

![End](images/image10.png)

<p>In general, we want the sum of all probabilities of all sentences of varying lengths to be 1, and we can achieve this using an end token. At the end of the sentence, we can insert an end token which introduces a new term in the sequence probability calculation which denotes the probability of a sentence to end with a particular word.</p>

![End_Token](images/image11.png)

# N-Gram Language Model

## Count Matrix

<p>First, we need to construct a count matrix using the corpus. For a bigram model, the rows denote the first word of the bigram and the columns denote the second word. We store the count of bigrams in these cells.</p>

![Count](images/image12.png)

## Probability Matrix

<p>Constructing the probability matrix from the count matrix is relatively simple, we divide each cell by the sum of all values of the row the cell is in.</p>

![Probability](images/image13.png)

## Language Model

<p>The language model uses the probability matrix to calculate sequence probabilities. We obtain the probability of each bigram from the probability matrix and calculate the product of all these probabilities.</p>

![Language](images/image14.png)

## Generative Language Model

<p>Using the generative language model, we find the most probable bigram at each step and keep generating bigrams till we encounter the end token.</p>

![Generative](images/image15.png)

# Language Model Evaluation

## Train Validation Test Split

<p>We should evaluate our model on data it has never seen before, so we split the data in 3 components, train, validation and test. We train our model on the training dataset and evaluate it using validation and test. We can split the data continuously or by taking random short sequences.</p>

![Split](images/image16.png)

## Perplexity

<p>Perplexity is a measure of how complex the sentence is. Higher the perplexity, more difficult it is to interpret the sentence. Human written sentences have low perplexities, and our model will be performing well if it has a low perplexity. We can calculate perplexity using the formula below.</p>

![Perplexity](images/image17.png)

<p>For bigram models:</p>

![Perplexity](images/image18.png)

# Out of Vocabulary Words

<p>We might encounter words that may not be in the vocabulary we construct using the training corpus. These words can be replaced by UNK tokens.</p>

<p>To create a vocabulary, we can include words which have a frequency higher than a threshold frequency and we can replace remaining words with UNK token.</p>

![Vocabulary](images/image19.png)

## Creating a Vocabulary

<p>Set a threshold frequency such that it allows the model to generalize but is also robust towards outliers. UNK tags shouldn't dominate the corpus or else the model will only predict these tokens. Lastly, we should only compare language models having the same vocabulary.</p>

![Creating](images/image20.png)

# Smoothing

<p>Sometimes, our training corpus may not have all probable N-grams and due to this, their probability is registered as 0. To avoid this, we can use smoothing techniques to ensure these N-grams don't have a zero probability.</p>

![Missing](images/image21.png)

<p>We can use Add-one smoothing or Add-k smoothing to smooth our data. Add-one is generally used for smaller text corpora whereas Add-k is used for bigger text corpora.</p>

![Laplacian](images/image22.png)

<p>In the Backing approach, if we encounter a zero probability for a N-gram, we consider the probability of (N-1)-gram and so on until we get a non-zero value. We generally multiply the non-zero value with a constant for a more realistic probability.</p>

![Backoff](images/image23.png)

<p>For interpolation, we consider a certain percentage of each sequence with decreasing lengths. We determine these percentages using the validationd data and choose values which maximize probabilities of sentences in validation data</p>

![Interpolation](images/image24.png)