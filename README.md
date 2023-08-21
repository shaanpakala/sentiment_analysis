# sentiment_analysis

*note: folders "saved_models" and "train_vectors" are not included since they are too big; however, all the files that are not included can be created by running the notebooks.


Random Forest Sentiment Analysis Model.
Input is a BOW representing the sentence(s). Normalized so that the sum of the BOW for the entire input is 1.
Output is a number -1 (negative sentiment), 0 (neutral sentiment), or 1 (positive sentiment).

Training data was acquired by collecting various sentences and their corresponding sentiments. Two datasets acquired by webscraping reviews from yelp.com and yellopages.com with their corresponding ratings. These ratings were converted so that 1-2/5 star is negative sentiment, 3/5 is neutral, and 4-5/5 is positive. Two more datasets were collected from kaggle. These two kaggle datasets are from twitter and reddit, both have the correspoding sentiment (negative, neutral, or positive) attached to the sentence(s). 

Vectorizing the training data into BOWs first entailed creating a word dictionary of all the words in all of the data. This dictionary was later refined so that words that appeared very rarely were removed (e.g. a proper noun that is only used in only one out of 50,000+ texts). This was done so that the model would not worry about irrelevant words which might affect the accuracy. It was also done to shorten the dictionary size for efficiency. Then using this dictionary, a BOW was created for each text so that each index of the vector corresponds to a specific word in the dicitonary. The value is the number of times that word shows up in the sentence divided by the total number of words in that sentence. This was done to ensure that short sentences and long sentences would not be drastically different simply because of the length of the sentence.

First round of training was done on the training data that was mentioned earlier, using a random forest classifier, with number of estimators set to 100. The training set was modified so that the data of each category had the same size (neutral, negative, and positive sentiment texts). This was done so that the classifier would not favor any specific category in training. 
This model achieved an overall accuracy of ~94% on test data. 
The following confusion matrix represents the percent of the true label in each predicted class (the sum of each row is 100%).

<img width="446" alt="Screen Shot 2023-08-20 at 10 16 14 PM" src="https://github.com/shaanpakala/sentiment_analysis/assets/68576257/6041dad9-fedd-43a3-9178-30fe064af372">

A second round of training was done on CNN political articles in order to fine tune this model in the field of political articles. 
This was done by first webscraping CNN articles from their website (~850 articles total). Then I manually filled in the sentiment of ~100 articles I webscraped. I fine tuned trained the random forest classifier model from before on this new train set of ~100 articles, expanding the number of estimators to 125. 

This second round of training was done so that I could attempt to detect any political bias in CNN's articles. I analyzed the distributions of predicted sentiments of CNN's articles on republicans and democrats separately. The results are shown in these two pie charts.

<img width="1035" alt="Screen Shot 2023-08-20 at 10 12 17 PM" src="https://github.com/shaanpakala/sentiment_analysis/assets/68576257/0e661c57-4dfc-4736-b56b-eb6fdb190682">
