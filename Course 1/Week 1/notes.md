# Supervised ML and Sentiment Analysis
## Steps required:
><ul>
><li>Extract Features from text</li>
><li>Train a classifier on the extracted features by minimizing the cost</li>
><li>Classify text documents</li>
></ul>
![Classifier Model](images/image1.png)

# Vocabulary and Feature Extraction
## Creaing Sparse Arrays in the manner shown below:
![Feature Representation](images/image2.png
)

# Postive and Negative Frequency
## We keep a track of the frequency of a word with reference to the classes(positive and negative).
<p>The mapping is done in a dictionary format from (word,class)->frequency</p>

![Positive Count](images/image3.png)
![Negative Count](images/image4.png)

# Feature Extraction with Tweets
## Creating a vector for a particular tweet using the method shown below:
![Encoding](images/image5.png) 
## Example:
![Example](images/image6.png)
# Text Preprocessing
1) Stop Words:
    <p>Words like "the", "that", etc that don't help the model classify a document are stop words. These words occur commonly because they have grammatical and syntactic impact but don't help the model classify the document. Removing stop words helps us preprocess the data</p>
![Stopwords_Example](images/image8.png)

2) Stemming:
    <p>There are many words that essentially convey the same meaning to the model but might have different forms. For example, run and running convey the same meaning, so the model should stem words like running to run to interpret them similarly.</p>
![Stemming_Example](images/image9.png)

# Putting it all together
## Steps involved:
><ul>
><li>Construct frequency dictionary by creating mappings from (word,class)->frequency</li>
><li>Iterate through all tweets and process them by removing stopwords, punctuations and by stemming them.</li>
><li>Create the vector as specified in Feature Extraction.</li>
![Pipeline_Preproc](images/image10.png)

# Overview of Logistic Regression
<p>Using parameters, we can predict an output labels with the help of the sigmoid function and then we can train our model to find parameters that lead to minimum loss.</p>

## Sigmoid Function
<p>Sigmoid function is used for binary classification and it's formula and graph can be seen below.</p>


![Sigmoid_Function](images/image11.png)

<p>We generally set a threshold of 0.5, i.e, if the output is greater than 0.5, we classify it as a positive label and if the output is lesser than 0.5, we classify it as a negative label.</p>

# Training Logistic Regression
<p>To train logistic regression, we use the Gradient Descent Algorithm to optimize values of the parameters in order to minimize the cost.</p>
 
![Training](images/image12.png)

![Training_Process](images/image13.png)

# Testing Logistic Regression
<p>To test our model, we divide the dataset into training and validation sets. Once we find parameter values after training the model on the training dataset, we compute labels of the validation dataset using these parameters.</p>

![Train_Val](images/image14.png)

<p>Then, to predict the accuracy of our model, we compare our predicted labels with the actual labels and find out how many labels we predicted correctly out of the total number of labels.</p>

![Accuracy](images/image15.png)

# Cost Function

<p>To understand the cost function, let's take a look at the equation and how it changes with different values.</p>

![Cost_Positive](images/image16.png)

![Cost_Negative](images/image17.png)

<p>From the graph, we observe that the cost function depends on how close is the predicted label to the true label</p>

