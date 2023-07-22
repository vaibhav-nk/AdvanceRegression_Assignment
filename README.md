# House Price Prediction For Surprise Housing
> A US-based housing company named Surprise Housing has decided to enter the Australian market. The company uses data analytics to purchase houses at a price below their actual values and flip them on at a higher price.

> The company is looking at prospective properties to buy to enter the market. You are required to build a regression model using regularisation in order to predict the actual value of the prospective properties and decide whether to invest in them or not.

> Essentially, the company wants —

> Which variables are significant in predicting the price of a house.
> How well those variables describe the price of a house


## Table of Contents
* [Python Libraries](#python-libraries)
* [Data Understanding](#data-Understanding)
* [Data Cleaning](#Data-Cleaning)
* [Data Exploration](#Data-Exploration)
* [Dummy Variables](#Dummy-Variables)
* [Data Preparation](#Data-Preparation)
* [Model BuildingEvaluate](#Model-BuildingEvaluate)

<!-- You can include any other section that is pertinent to your problem -->

## python-libraries
- To perform the EDA on the given dataset we are using python libraries like
  numpy, pandas
- For plotting the extracted data on different graphs we will using below libraries
  seaborn, matplotlib
- For builting a linear regression model with ridge & lasso we will using below libraries
  sklearn

## Data Understanding
- Shape: Data set has 1460 rows and 81 features.
- Details 
  - Dataset has important features which will be considered in this analysis.
  - Numerical features: 'MSSubClass', 'LotFrontage', 'LotArea', 'OverallQual', 'OverallCond', 'BuiltAge', 'RemodAddAge', 'MasVnrArea',
    'BsmtFinSF1', 'BsmtFinSF2', 'BsmtUnfSF', 'TotalBsmtSF', '1stFlrSF', '2ndFlrSF', 'LowQualFinSF', 'GrLivArea', 'BsmtFullBath',
    'BsmtHalfBath', 'FullBath', 'HalfBath', 'BedroomAbvGr', 'KitchenAbvGr', 'TotRmsAbvGrd', 'Fireplaces', 'GarageBltAge', 'GarageCars',
    'GarageArea', 'WoodDeckSF', 'OpenPorchSF', 'EnclosedPorch', '3SsnPorch', 'ScreenPorch', 'PoolArea', 'MiscVal', 'MoSold',
    'SoldAge', 'SalePrice'.
  - Categorical features: 'MSZoning', 'Street', 'Alley', 'LotShape', 'LandContour', 'Utilities', 'LotConfig', 'LandSlope','Neighborhood', 'Condition1', 'Condition2', 'BldgType', 'HouseStyle', 'RoofStyle', 'RoofMatl', 'Exterior1st', 'Exterior2nd',  'MasVnrType', 'ExterQual', 'ExterCond', 'Foundation', 'BsmtQual', 'BsmtCond', 'BsmtExposure', 'BsmtFinType1', 'BsmtFinType2', 'Heating', 'HeatingQC', 'CentralAir', 'Electrical', 'KitchenQual', 'Functional', 'FireplaceQu', 'GarageType', 'GarageFinish', 'GarageQual', 'GarageCond', 'PavedDrive', 'PoolQC', 'Fence', 'MiscFeature', 'SaleType', 'SaleCondition'.

## Data Cleaning
- Missing Values
  - There are features like 'PoolQC', 'Fence', 'MiscFeature' has missing values greater than 60%, and hence these are removed from dataset.
  - There are features like 'MSZoning', 'Neighborhood', 'BldgType', 'Exterior2nd' has wrong values, those are corrected as per dictionary.
  - There are features like 'Alley', 'MasVnrType', 'MasVnrArea', 'LotFrontage', 'Fireplaces', 'GarageArea', 'BsmtFinType2',     'Electrical', 'BsmtQual','BsmtCond','BsmtExposure','BsmtFinType1','BsmtFinType2', 'GarageType','GarageFinish','GarageQual','GarageCond' has missing values, those are filled with the help from dictionary.
  - Datatype for GarageYrBlt changed to int.
  - Age calculated for YearBuilt, YrSold, GarageYrBlt, YearRemodAdd
  - There are no duplicate values in the dataset.

## Data Exploration
- Data Type Analysis: 
  - Features like 'MSSubClass', 'OverallQual', 'OverallCond' are having integer values but actually they have categorical values, so datatype changed to string.
  - With the help of heat map it is found that 
    - Correlation of price with independent variables:
        - House Sale Price is highly (positively) correlated with GrLivArea, GarageCars, GarageArea, TotalBsmtSF, 1stFlrSF, fullBath, TotRmsAbvGrd, YearBuilt, YearRemodAdd, FirePlaces, MasVNrArea, BsmtFinSF1, WoodDeckSF, OpenPorchSF, 2ndFlrSF, HalfBath, LotArea, BsmtFullBath, LotFrontage, BsmtUnfSF, BedroomAbvGrd. Also features which are very less liked by the customers are ScreenPorch, 3SsnPorch, MoSold, PoolArea.

        - Houce Sale Price is negatively correlated to KitchenAbvGr, EnclosedPorch, BsmtFinSF2, BsmtHalfBath, MiscVal, LowQualFinSF, YrSold. This suggest that houses having kitchen above grade are mostly disliked by the customers, and have low price.
    - Correlation among independent variables:
        Many independent variables are highly correlated. TotalBsmtSF, 1stFlrSF, TotalRmsAbvGr, GrLivArea etc are positively correlated.
        This multicollinearity will be handled in regualarization process in Ridge & Lasso Regression.

## Data Preparation
- Dataset splitted into X and y datasets.
- Id column has no significance in analysis as its a unique column and has no corelation with any other feature.
- Dummy variables are created for all the above mentioned categorical variables and original categorical variables are removed.
- Scaling done for all the features.
- Using sklearn library split dataset data into training (70% data) and testing (30% data) sets

## Model BuildingEvaluate
  - Linear regression model created and prediction for output variable on both training and test dataset done.
  - The metrics found are as follows:
    - R2 Score (train): 0.9569162986296403
    - R2 Score (test): -2.702252107141158e+21
    - RSS Value (train): 43.58860581588001
    - RSS Value (test): 1.2077258927401444e+24
    - MSE Value (train): 0.04269207229762978
    - MSE Value (test): 2.7573650519181377e+21
  - There is a overfitting problem in above model. Features present in model 278.
  
  - Ridge regression model created and used 28 different values of alpha (ranging between 0.0001 to 1000) for tunning.
  - The best value for hyperparameter alpha is found as 500.
  - The metrics found are as follows:
    - R2 Score (train): 0.8936084915279175
    - R2 Score (test): 0.8624484872054756
    - RSS Value (train): 107.638326732459
    - RSS Value (test): 61.47632308196268
    - MSE Value (train): 0.10542441403766797
    - MSE Value (test): 0.14035690201361342
  - The difference in R2 score is 3.49%. Model is complex as it has 275 features.

  - Lasso regression model created and used 28 different values of alpha (ranging between 0.0001 to 1000) for tunning.
  - The best value for hyperparameter alpha is found as 0.01.
  - The metrics found are as follows:
    - R2 Score (train): 0.9066942909483535
    - R2 Score (test): 0.8439611774567116
    - RSS Value (train): 94.39917283944024
    - RSS Value (test): 69.73891361216718
    - MSE Value (train): 0.09245756399553402
    - MSE Value (test): 0.15922126395471958
  - The difference in R2 score is 6.91%, so overfitting problem still present. Model is less complex as it has 113 features.

## Contact
Created by [@vaibhav-nk] - feel free to contact me!


<!-- Optional -->
<!-- ## License -->
<!-- This project is open source and available under the [... License](). -->

<!-- You don't have to include all sections - just the one's relevant to your project -->