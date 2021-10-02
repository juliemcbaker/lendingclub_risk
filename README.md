# lendingclub_risk

Supervised learning models were built and validated using a subset of 2019 loan data from Lending Club [^1]. The models were there then tested on  first quarter data from 2020.

The specific subsets of data used can be found here:
[2019] (Resources/2019loans.csv)
[2020Q1] (Resources/2020Q1loans.csv)

## Preprocessing
1. data for the two years were checked for column consistency 
2. pd.get_dummies() was then used to transform categorical data into binary columns
3. columns were then compared again after transformation
  - 2020 data generated an extra column 'debt_settlement_flag_Y' 
  - this 'debt_settlement_flag_Y' column had perfect covariance with 'debt_settlement_flag_N' which appeared in both years
  - the 'debt_settlement_flag_Y' column was generated for the 2019 data based upon the values in 'debt_settlement_flag_N'

## Consider the models...

### Which model will perform better: logistic regression or random forests classifier?

* I predict the Random Forest will outperform the Logistic Regression. I'm grounding this in 2 scholarly articles I
found online that said Random Forest models increasingly outperform Logistic Regression.

* <https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2264-5>
* <https://scholar.smu.edu/cgi/viewcontent.cgi?article=1041&context=datasciencereview>

## Training unscaled models
### Logistic regression (unscaled)
* X variable for 2019 was created by dropping the 'target_high_risk' and 'target_low_risk' columns from the train_convert_df
* y variable for 2019 was defined as the 'target_high_risk' column from the train_convert_df
* array shapes were compared to verify compatibility {Shape:  (12180, 92) (12180,)}
* X_20 variable for 2020 was created by dropping the 'target_high_risk' and 'target_low_risk' columns from the test_convert_df
* y_20 variable for 2020 was defined as the 'target_high_risk' column from the test_convert_df
* array shapes were compared to verify compatibility {Shape:  (4702, 92) (4702,)}
* train_test_split was used to divide the 2019 data into a training & testing subsets
* LogisticRegression(max_iter=20000) was used to train the model

#### Scores for unscaled logistic regression
| Score Type           | Score             |
|----------------------|-------------------|
|Training Data Score   |0.7094690749863164 |
|Testing Data Score (from training set) |0.69688013136289 |
|First Quarter 2020 fit | 0.5546575925138238| 

### Random Forest Classifier Model (unscaled)
* the model was trained using random_state=7 and n_estimators=500

#### Scores for unscaled random forest classifier
| Score Type           | Score             |
|----------------------|-------------------|
|Training Data Score   |1.0 |
|Testing Data Score (from training set) |0.7878489326765189 |
|First Quarter 2020 fit | 0.6461080391322841| 

### Results
* As predicted, the random forest model outperformed the logistic regression model. 
* Logistic regression had Training Score: 0.71, Testing Score (from training set): 0.70, and more important First Quarter 2020 fit: 0.55
* Random forest had Training Score: 1.0, Testing Score (from training set): 0.79, and First Quarter 2020 fit: 0.65

[^1] LendingClub (2019-2020) _Loan Stats_. Retrieved from: [https://resources.lendingclub.com/](https://resources.lendingclub.com/)
