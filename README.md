# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs, NLP, & Classification Models

### Executive Summary

I am a data scientist and a digital marketing company has hired me to build a model to classify post titles between subreddits as accurately as possible. This company is interested specifcilally in the two subreddits, [AskWomen](https://www.reddit.com/r/AskWomen/) and [AskMen](https://www.reddit.com/r/AskMen/). They are interested in the differences in the post titles for the two groups to help them make their advertisements on each thread more relevant. My classification models will predict which subreddit the post title belongs to. The model results will also show us which words are used most frequently in AskWomen or AskMen posts. 

---

### Datasets

The 3 datasets included in the [`Data`](./Data/) folder were used for this project and described below. 

* [`women.csv`](./Data/women.csv): AskWomen cleaned posts
* [`men.csv`](./Data/men.csv): AskMen cleaned posts
* [`cleaned.csv`](./Data/cleaned.csv): women and men posts cleaned and combined

---

### Data Dictionary (Full Dataset)

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**title**|*string*|cleaned|post title from Reddit thread| 
|**subreddit**|*int*|cleaned|binary classification if title belongs to AskWomen or AskMen thread| 

---

### Methodology 

I used [Pushshift's API](https://github.com/pushshift/api) to collect the post titles in the AskWomen and AskMen subreddits. Based on their documentation, I set up a function to pull down the titles for about 50,000 posts on each thread. I set my filters to remove posts that were previously removed and also filter the content to be more appropriate for a work setting. This process can be found in the data_collection notebook. 

After I collected the posts, I made a cleaning function to pass each set of data through. I removed duplicate posts, posts with less than two words, filtered out other unnecessary posts, and tokenized the sentences to remove capitalization and punctuation. The threads that indicate where the post came from was binarized, 1 for AskWomen and 0 for AskMen. Then I combined all posts into one full dataset and exported the full dataset to a csv. I also made counts of the number of words and characters in each post and made histograms to view trends between threads. I made bar charts for the most used words in each subreddit and combinded full data set. I also experimented with count vecorizer, tf-idf, bi-grams and tri-grams, and stop words. This code can be found in the data_clean_and_eda notebook.

After the data was cleaned, I could import this and test out which classification models performed best for my specific problem. In the different notebooks, there are variations of Naive Bayes, Random Forest Classifiers, Logistic Regression, and Support Vector Classifiers. 

To evaluate which classification model is the best for classifying which thread a post belongs to, I used the criteria below:
 - Does the model score better than the baseline?
 - How does the model’s accuracy score compare to other models?
 - How do the accuracy scores for training and testing groups compare to each other and other models?
 - Can we make any inferences from the results?
 - How much time and computing resources does the model require to run?

---

### Conculsions and Recommendations

We hit our upper limit on the accuracy rate for classifying posts between the AskWomen and AskMen subreddits. This is clear from the numerous types of classification models that were explored. My client and I can feel confident that the Naive Bayes production model chosen yields the most accurate resutls possible for the data set. This model was chosen because the training data scored an .75 accuracy rate and the testing data scored a .72 accuracy rate. This outperforms the baseline model of a .5 accuracy rate. It also has the best score on testing data compared to other models. Plus, many of the other models were greatly overfit whereas this model performs similarly on seen and unseen data. This model also has an advantage compared to other models because it takes less time to run on large datasets. 

When looking at the results, I was surprised that the upper limit in accuracy scores on testing data was in the low 70s. When digging into this deeper, I looked at the frequency of most common words used in both subreddits. It's clear that topics of conversation between AskWomen and AskMen are similar. The words used most frequently in both subreddits focus on interpersonal relationships. It's important to keep the similarity of subreddits and that this may impact the classification accuracy. 

A key take away from this study is that my client can use similar digital marketing may be used for the AskWomen and AskMen subreddits since they have related topics of converstion in the posts. Also, the efficient pipelines created for data cleaning and the production model are set up and can be used to compare other subreddits for future marketing purposes.
