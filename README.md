# Sentiment Analysis

*note: folders "saved_models" and "train_vectors" are not included since they are too big; however, all the files that are not included can be created by running the notebooks.


Random Forest Sentiment Analysis Model.
Input is a BOW representing the sentence(s). Normalized so that the sum of the BOW for the entire input is 1.
Output is a number -1 (negative sentiment), 0 (neutral sentiment), or 1 (positive sentiment).

Training data was acquired by collecting various sentences and their corresponding sentiments. Two datasets acquired by webscraping reviews from yelp.com and yellowpages.com with their corresponding ratings. From both websites, reviews were acquired from various cities across the United States and from various business types. These ratings were converted so that 1-2/5 star is negative sentiment, 3/5 is neutral, and 4-5/5 is positive. Two more datasets were collected from kaggle. These two kaggle datasets are from twitter and reddit, both have the correspoding sentiment (negative, neutral, or positive) attached to the sentence(s). 

Vectorizing the training data into BOWs first entailed creating a word dictionary of all the words in all of the data. Adverbs (such as 'really' and 'very') and the word 'not' had the following word in the sentence attached to the end, since context matters a lot for these words. For example, the phrase "not good" would go into the dictionary as one word "not_good."

This dictionary was later refined so that words that appeared very rarely were removed (ideally misspelled words are removed, but generally words that are rarely used). This was done so that the model would not worry about irrelevant words which might affect the accuracy. It was also done to shorten the dictionary size for efficiency. Then using this dictionary, a BOW was created for each text so that each index of the vector corresponds to a specific word in the dicitonary. The value is the number of times that word shows up in the sentence divided by the total number of words in that sentence. This was done to ensure that short sentences and long sentences would not be drastically different simply because of the length of the sentence.

First round of training was done on the training data that was mentioned earlier, using a random forest classifier, with number of estimators set to 100. The training set was modified so that the data of each category had the same size (neutral, negative, and positive sentiment texts). This was done so that the classifier would not favor any specific category in training. The modifications to the train set was done randomly.
This model achieved an overall accuracy of ~98% on test data. 
The following confusion matrix represents the percent of the true label in each predicted class (the sum of each row is 100%).

<img width="560" alt="Screen Shot 2023-08-27 at 9 53 57 PM" src="https://github.com/shaanpakala/sentiment_analysis/assets/68576257/02c2501f-8651-4498-a13f-9b6117d00d45">


