# What's the Subreddit?
A study of using Natural Language Processing, APIs and classification models to see where a post comes from.

# Executive Summary

## Problem Statement

Can we classify which subreddit a post or comment come from using NLP and machine learning?

## Summary

Using the [PRAW API](https://praw.readthedocs.io/en/latest/index.html), I was about to get the top 1,000 posts from /r/bitcoin and /r/wallstreetbets.  From these 1,000 posts, I pulled the comments for each.  After removing the deleted comments, I put used the TfidfVectorizer on each dataset before putting it into a model.  I used three different data sets: post titles, comments and comments with "self-text" (a post where the submitter made a comment).  Each was ran in three different types of models with a gridsearch: Logistic Regression, Bernoulli Naive Bayes, and a Support Vector Classifier.  For the latter two datasets, I sampled 20,000 rows from each subreddit because trying to run a model from over 1,000,000 rows was taking too long on my computer.  The best results came from the title dataset with each model having the same score on the testing data.  The SVC scored 75% on the training set and 64% on the testing set.  This score is too low to really do anything with and I would need to continue to tune the model.

### Gridsearch Parameters:

| Parameter | Options |
|---|---|
| Max Features | 2,500, 5,000, None |
| NGram Range | (1,1), (1,2) |
| Max DF | 90%, 95% |
| Min DF | None, 5% |
| Stop Words | None, English |
|SVC Kernel | RBF, Polynomial |
| SVC Degrees | 2, 3|

Dialing in more of the features and iterating more could yield better results.  Additionally, using cloud computing and AWS could allow me to use a larger dataset in a reasonable amount of time.  Also, looking at more recent posts than just the all-time top posts should help narrow down results because language and terms can change over time in these subreddits.  When both involved looking at current events recency can be important.  
