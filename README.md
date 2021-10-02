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
5. hold

## 


[^1] LendingClub (2019-2020) _Loan Stats_. Retrieved from: [https://resources.lendingclub.com/](https://resources.lendingclub.com/)
