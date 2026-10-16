Model Card: Bank Term Deposit Ranking

Author:saduakas  
Student ID: 2345  

1. Purpose

The purpose of this model is to rank bank clients by their chance of saying yes to a term deposit. The call centre can contact only 10% of the clients. The model helps select clients with higher scores.

I use Average Precision as the main metric and ROC-AUC as a second metric.

2. Data

The project uses the UCI Bank Marketing dataset. The training data contains 32,940 rows, and the test data contains 8,236 rows. The share of yes answers in the training data is about 11.3%.

I use only features that are available in the test data. I do not use the ID as a feature. If duration is not available in the test data, I exclude it because it is known only after a call.

3. Preprocessing and Model

Numerical features are filled with the median and scaled with StandardScaler. Categorical features are encoded with OneHotEncoder.

The value unknown is handled by **[your selected method]**. The value pdays = 999 is replaced with the median, and a missing indicator is added.

All preprocessing steps are inside a scikit-learn Pipeline. This helps prevent data leakage during cross-validation.

The selected model is [model name]. Its main settings are [best parameters]. Class imbalance is handled by [your choice].

#4. Validation and Results

I used an 80/20 stratified split. The 80% training part was evaluated with five-fold StratifiedKFold.

The majority-class baseline had an accuracy of [value], ROC-AUC of [value], and AP of [value].

The selected model had a mean CV AP of [value] with a standard deviation of [value]. Its mean ROC-AUC was [value].

On the hold-out data, ROC-AUC was [value] and AP was [value]. When I selected the top 10% of clients, precision was [value], recall was [value], and lift was [value].

5. Limitations

The data come from campaigns between 2008 and 2010. A random split may give better results than predicting a completely new period.

Only 10% of clients can be contacted, so some positive clients will be missed. The economy and client behaviour may change over time.

The model has not been fully checked for fairness across age and job groups. The results should not be treated as conclusions about all real bank clients.

6. Monitoring

If the model is used in the future, I would monitor the yes rate among contacted clients, the distribution of scores, and the share of unknown values.

I would also check performance on new campaign data and retrain the model when its performance becomes worse.