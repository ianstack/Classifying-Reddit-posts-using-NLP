# <span style="font-variant:small-caps;">Project 3 - Web APIs & NLP:</span>
#### <span style="font-variant:small-caps;">Ian Stack</span>

---

## Executive Summary

### Contents:
-[Problem Statement](#Problem-Statement)

-[Description of Data](#Description-of-Data)

-[Conclusions and Recommendations](#Conclusions-and-Recomendations)

---
### <span style="font-variant:small-caps;">Problem Statement</span> 
Can I predict which subreddit posts came from r/nhl vs. r/nba?

Professional sports has become one of the biggest entertainment businesses and captures indviduals all over the world. In particular, the professional sports league: NHL and NBA are well known leagues with multiple teams throughout the United States. Both the NBA and NHL have a large fanbase and opinions are commonly shared on reddit. I was hired by both the NBA and NHL to review the subreddit pages per each league and ensure that operations are running correctly. It is my job to make sure that individual's posts are being posted on the correct subreddit.

In this project I will be utilizing Pushshit Reddit API to obtain the "NBA" and "NHL" subreddit pages from Reddit. I will utilize Multinominal Naive Bayes, K-nearest Neighbor, and Logistic Regression modeling and will be evaluated via accuracy on predicting whether the user's post came from r/nba or r/nhl.

### Goal

I will be able to predict whether the subreddit post came from r/nba or r/nhl.

### Description of Data

#### Datasets
From The "r/nba" subreddit, I created a dataframe with 3000 rows and saved it as 'nba_new.csv'.  I then created another dataframe of 3000 rows from the "r/nhl" subreddit page and saved it as 'nhl_new.csv'.  For both of these dataframes, the only columns that I used where the 'subreddit', 'title', and 'selftext'.  With only using these columsn I merged these two datasets and saved it as, 'subreddit_merged.csv'.  All three off the saved datasets can be found in the dataset folder.  The orginal reddit data was pulled from the 'p3_datasets'.
 

#### Source
Reddit:
- r/nba
- r/nhl


### <span style="font-variant:small-caps;">Data Dictionary</span>
|Feature|Type|Dataset|Description|
|---|---|---|---|
|subreddit|object|subreddit|Title of Subreddit|
|selftext|object|subreddit|Text in something|
|title|object|subreddit|Title of Reddit post|
|label|integer|subreddit|Subreddit into binary labels (NBA = 1 and NHL = 0)|
|total_text|object|subreddit|Selftext and Title columns combined|
|tokenized|object|subreddit|Tokenized sentences from total_text|
|total_text_length|integer|subreddit|Count of total_text characters|
|total_text_word_count|integer|subreddit|Word count for total_text|

### <span style="font-variant:small-caps;">Brief Analysis</span>
I started my analysis by looking over the merged dataset and seeing what key words were constantly used for certain subreddit's.  From this point I began my exploratory data analysis and looked for trends amongst the data. 


### <span style="font-variant:small-caps;">Model Performance on Training/Test Data</span>
In total I fitted 6 different models.  I pefromed 3 types of modeling tests with 2 different vectorizers.  I also provided the sensitivity and specificity scores per each test.

| Model | Train Score | Test Score | Sensitivity | Specificity |
| --- | --- | --- | --- | --- |
| Multinomial Bayes (Count Vectorizer) | 0.946 | 0.923 | 0.901 | 0.945 |
| Multinomial Bayes (TF-IDF Vectorizer) | 0.956 | 0.927 | 0.906 | 0.947 |
| K-Nearest Neighbor (Count Vectorizer) | 0.844 | 0.777 | 0.606 | 0.944 |
| K-Nearest Neighbor (IF-IDF Vectorizer) | 0.505 | 0.505 | 1.0 | 0.0 |
| Logistic Regression (Count Vectorizer) | 0.929 | 0.908 | 0.849 | 0.966 |
| Logistic Regression (IF-IDF Vectorizer) | 0.929 | 0.908 | 0.849 | 0.966 |


### <span style="font-variant:small-caps;">Conclusions and Recommendations</span>

Overall I would conclude that my models are overfit based on the Train RMSE being greater than the Test RMSE in all but
one model.  I think this had to do with the fact that "nba" or "nhl" must have occured in many of the subreddit
posts.

I found that Multinomial Bayes was the best model, specfically the one used with TF-IDF Vectorizer.  I also found the
sensitivity, the probability of a positive test, and the specificity, the pprobaility of a negative test.  In my model I
had a positive test be 1, which is correctly identifying the subreddit was r/nba.  For both Multinomial Bayes
model, the specificity was higher than the sensitivity.

Futhermore, I created a y-actual vs. y-pred table to see what rows my model predicted wrong and the text it 
went off.  I saw that a lot of my errors had to do with professional athlete names.  I also saw that some of the posts
had words that could be used in both subreddit's such as the words: 'game', 'score', and 'points'.

In Conclusion, based off my Multinomial Bayes (TF-IDF Vectorizer) model, I would conclude that the users posts are 
indeed be posted on the correct subreddit.  NBA related posts are being posted on r/nba and NHL related posts
are being posted on r/NHL.  Both of these professional sports leage reddit pages are running correctly.

Next Steps:

    - adjust stop words: adjust common words such as: 'game', 'score', and 'points'
    
    - more cleaning on emoji's, pictures, and videos in subreddit posts
    
    - adjust the names of professional atheltes quoted in subreddit posts