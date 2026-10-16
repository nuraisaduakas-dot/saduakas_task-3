
1. Purpose
The purpose of this model is to rank bank clients by their chance of saying yes to a term deposit. The call centre can contact only 10% of the clients. The model helps select clients with higher scores.

I use Average Precision as the main metric and ROC-AUC as a second metric.

2. Data
The project uses the UCI Bank Marketing dataset. The training data contains 32,940 rows, and the test data contains 8,236 rows. The share of yes answers in the training data is about 11.3%.

I use only features that are available in the test data. I do not use the ID as a feature. If duration is not available in the test data, I exclude it because it is known only after a call.

3. Preprocessing and Model
Numerical features are filled with the median and scaled with StandardScaler. Categorical features are encoded with OneHotEncoder.

The value unknown is handled by kept as a separate category. The value pdays = 999 is replaced with the median, and a missing indicator is added.

All preprocessing steps are inside a scikit-learn Pipeline. This helps prevent data leakage during cross-validation.

The selected model is Random Forest. Its main settings are max_depth=12, min_samples_leaf=5. Class imbalance is handled by not used (default class weights).

4. Validation and Results
I used an 80/20 stratified split. The 80% training part was evaluated with five-fold StratifiedKFold.

The majority-class baseline had an accuracy of 0.8873, ROC-AUC of 0.5000, and AP of 0.1127.

The selected model had a mean CV AP of 0.4617 with a standard deviation of 0.0144. Its mean ROC-AUC was 0.7986.

On the hold-out data, ROC-AUC was 0.8075 and AP was 0.5166. When I selected the top 10% of clients, precision was 0.5456, recall was 0.4838, and lift was 4.84.

5. Limitations
The data come from campaigns between 2008 and 2010. A random split may give better results than predicting a completely new period.

Only 10% of clients can be contacted, so some positive clients will be missed. The economy and client behaviour may change over time.

The model has not been fully checked for fairness across age and job groups. The results should not be treated as conclusions about all real bank clients.

6. Monitoring
If the model is used in the future, I would monitor the yes rate among contacted clients, the distribution of scores, and the share of unknown values.

I would also check performance on new campaign data and retrain the model when its performance becomes worse.