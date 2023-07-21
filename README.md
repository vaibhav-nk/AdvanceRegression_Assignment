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
- Shape
  Data set has 1460 rows and 81 features.
- Details
  Dataset has important features which will be considered in this analysis.
  Numerical features: 'MSSubClass', 'LotFrontage', 'LotArea', 'OverallQual', 'OverallCond', 'YearBuilt', 'YearRemodAdd', 'MasVnrArea',
 'BsmtFinSF1', 'BsmtFinSF2', 'BsmtUnfSF', 'TotalBsmtSF', '1stFlrSF', '2ndFlrSF', 'LowQualFinSF', 'GrLivArea', 'BsmtFullBath',
 'BsmtHalfBath', 'FullBath', 'HalfBath', 'BedroomAbvGr', 'KitchenAbvGr', 'TotRmsAbvGrd', 'Fireplaces', 'GarageYrBlt', 'GarageCars',
 'GarageArea', 'WoodDeckSF', 'OpenPorchSF', 'EnclosedPorch', '3SsnPorch', 'ScreenPorch', 'PoolArea', 'MiscVal', 'MoSold',
 'YrSold', 'SalePrice'.
  Categorical features: 'MSZoning', 'Street', 'Alley', 'LotShape', 'LandContour', 'Utilities', 'LotConfig', 'LandSlope', 'Neighborhood',
 'Condition1', 'Condition2', 'BldgType', 'HouseStyle', 'RoofStyle', 'RoofMatl', 'Exterior1st', 'Exterior2nd', 'MasVnrType', 'ExterQual',
 'ExterCond', 'Foundation', 'BsmtQual', 'BsmtCond', 'BsmtExposure', 'BsmtFinType1', 'BsmtFinType2', 'Heating', 'HeatingQC', 'CentralAir', 'Electrical', 'KitchenQual', 'Functional', 'FireplaceQu', 'GarageType', 'GarageFinish', 'GarageQual', 'GarageCond',
 'PavedDrive', 'PoolQC', 'Fence', 'MiscFeature', 'SaleType', 'SaleCondition'.

## Data Cleaning
- Missing Values
  There are features like 'PoolQC', 'Fence', 'MiscFeature' has missing values greater than 60%, and hence these are removed from dataset.
  There are features like 'MSZoning', 'Neighborhood', 'BldgType', 'Exterior2nd' has wrong values, those are corrected as per dictionary.
  There are features like 'Alley', 'MasVnrType', 'MasVnrArea', 'LotFrontage', 'Fireplaces', 'GarageArea', 'BsmtFinType2', 'Electrical', 'BsmtQual','BsmtCond','BsmtExposure','BsmtFinType1','BsmtFinType2', 'GarageType','GarageFinish','GarageQual','GarageCond' has missing values, those are filled with the help from dictionary.
  Datatype for GarageYrBlt changed to int.
  There are no duplicate values in the dataset.

## Data Exploration
- Data Type Analysis
  Features like 'MSSubClass', 'OverallQual', 'OverallCond' are having integer values but actually they have categorical values, so datatype changed to string.
  With the help of heat map it is found that 
    Correlation of price with independent variables:
        House Sale Price is highly (positively) correlated with GrLivArea, GarageCars, GarageArea, TotalBsmtSF, 1stFlrSF, fullBath, TotRmsAbvGrd, YearBuilt, YearRemodAdd, FirePlaces, MasVNrArea, BsmtFinSF1, WoodDeckSF, OpenPorchSF, 2ndFlrSF, HalfBath, LotArea, BsmtFullBath, LotFrontage, BsmtUnfSF, BedroomAbvGrd. Also features which are very less liked by the customers are ScreenPorch, 3SsnPorch, MoSold, PoolArea.

        Houce Sale Price is negatively correlated to KitchenAbvGr, EnclosedPorch, BsmtFinSF2, BsmtHalfBath, MiscVal, LowQualFinSF, YrSold. This suggest that houses having kitchen above grade are mostly disliked by the customers, and have low price.
    Correlation among independent variables:
        Many independent variables are highly correlated. TotalBsmtSF, 1stFlrSF, TotalRmsAbvGr, GrLivArea etc are positively correlated.
        This multicollinearity will be handled in regualarization process in Ridge & Lasso Regression.

## Data Preparation
- Dataset splitted into X and y datasets.
- Id column has no significance in analysis as its a unique column and has no corelation with any other feature.
- Dummy variables are created for all the above mentioned categorical variables and original categorical variables are removed.
- Scaling done for all the features.
- Using sklearn library split dataset data into training (70% data) and testing (30% data) sets

## Model BuildingEvaluate
  Linear regression model created and prediction for output variable on both training and test dataset done.
  The metrics found are as follows:
    R2 Score (train): 0.9569161787029803
    R2 Score (test): -8.05901679608141e+21
    RSS Value (train): 274904886826.7783
    RSS Value (test): 2.271605162541836e+34
    MSE Value (train): 269250623.7284802
    MSE Value (test): 5.18631315648821e+31
  There is a overfitting problem in above model. Features present in model 278.
  
  Ridge regression model created and used 28 different values of alpha (ranging between 0.0001 to 1000) for tunning.
  The best value for hyperparameter alpha is found as 500.
  The metrics found are as follows:
    R2 Score (train): 0.8936641677004936
    R2 Score (test): 0.862558947239897
    RSS Value (train): 678496917494.8549
    RSS Value (test): 387406817599.4418
    MSE Value (train): 664541545.0488294
    MSE Value (test): 884490451.140278
  The difference in R2 score is 3%. Model is complex as it has 278 features.

  Lasso regression model created and used 28 different values of alpha (ranging between 0.0001 to 1000) for tunning.
  The best value for hyperparameter alpha is found as 500.
  The metrics found are as follows:
    R2 Score (train): 0.9322771190403039
    R2 Score (test): 0.8475354701397759
    RSS Value (train): 432119305236.66144
    RSS Value (test): 429753680750.98413
    MSE Value (train): 423231444.8938897
    MSE Value (test): 981172787.1027035
  The difference in R2 score is 9%, so overfitting problem still present. Model is less complex as it has 142 features.

## Contact
Created by [@vaibhav-nk] - feel free to contact me!


<!-- Optional -->
<!-- ## License -->
<!-- This project is open source and available under the [... License](). -->

<!-- You don't have to include all sections - just the one's relevant to your project -->