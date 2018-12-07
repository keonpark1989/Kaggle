What preprocessing and supervised learning methods did you use?


Relevance를 예측하는 모델 
* Query와 아이템 타이틀과 겹치는 단어들의 갯수
* Query 길이, Jacquard similarity
* 같이 등장하는 단어들 
* 단어들의 similarities
The key to this competition was mostly preprocessing and feature engineering as the primary data is text. Our processed text features can broadly be grouped into a few categories: categorical features, counting features, co-occurrence features, semantic features, and statistical features.
* Categorical features: Put words in categories such as colors, units, brands, core. Count the number of those words in the query/title and count number of intersection between query and title for each category.
* Counting features: Length of query, number of common grams between query and title, Jacquard similarity, etc.
* Co-occurrence features: Measures of how frequently words appear together. e.g., Latent Semantic Analysis (LSA).
* Semantic features: Measure how similar the meaning of two words is.
* Statistical features: Compare queries with unknown score to queries with known relevance score.
It seems that a lot of the top teams had similar types of features, but the implementation details are probably different. For our ensemble we used different variations of xgboost along with a ridge regression model.
RIDGE REGRESSION????? 
* What is it?
* When to use it
WORD CLOUD OF HOME DEPOT PRODUCT SEARCH TERMS.
For models and ensemble we started with random forest, extra trees and gbm-models. Furthermore xgboost and ridge were in our focus. Shortly prior to the end of the competition we found out, that first random forest and then extra trees did not help our ensembles anymore. So we focused on xgboost, gbm and Ridge.

Our best single model was a xgboost-model and scored 0.43347 on the public LB. The final ensemble consists of 19 models based on xgboost, gbm and Ridge. The xgboost-models were made with different parameters including binarizing the target, objective reg:linear, and objective count:poisson. We found, that the Ridge Regression helped in nearly every case, so we included it in the final ensemble.
OUR DATA PROCESSING PIPELINE.
Were you surprised by any of your findings?

A surprising finding was the large number of features which had predictive ability. In particular, when we teamed up, it was better to combine our features than to ensemble our results. This is quite unique as most of the time new features are more likely to cause overfit but not in this case. As a result, adding more members to the team was highly likely to improve score which is why the top-10 were all teams of at least 3 people.
Which tools did you use?

We used mainly Python 3 and Python 2. The decision for Python 2 is interesting as some of the used libraries are still not available for Python 3. In our processing chain we used the Python standard tools for machine learning (scikit-learn, nltk, pandas, numpy, scipy, xgboost, gensim). Nima used R for feature generation.
How did you spend your time on this competition?

After teaming up, Sean and Nima spent most of their time on feature engineering and Thomas and Qingchen spent most of their time on model tuning.
What was the run time for both training and prediction of your winning solution?

In general, training/prediction time is very fast (minutes), but we used some xgboost parameters that took much longer to train (hours) for small performance gains. Text processing and feature engineering took a very long time (easily over 8 hours for a single feature set).
Words of wisdom

What have you taken away from this competition?

First of all quite a lot of Kaggle ranking points and Thomas got his Master badge! Overall this was a very difficult competition and we learned a lot about natural language processing and information retrieval in practice. It now makes sense why Google is able to use such a large number of features in their search algorithm as many seemingly insignificant features in this competition were still able to provide a tangible performance boost.


KP Approach
* W2v vectorization -> cosine similarity, jacquard similarity
* RandomForest
* XGBoost
