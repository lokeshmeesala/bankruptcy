# Predict Bankruptcy of companies based on financial features

## Problem Statement: 
You have to build a model on the basis given features and target column to predict whether a company is going to get bankrupt based on a given set of features.

Data Set Information:
The dataset is about bankruptcy prediction of Polish companies. The data was collected from Emerging Markets Information Service (EMIS, [Web Link]), which is a database containing information on emerging markets around the world. The bankrupt companies were analysed in the period 2000-2012, while the still operating companies were evaluated from 2007 to 2013.

There are 64 features in the data. Some of the features are net profit, total liabilities, working capital, assets, earnings, sales, profits, EBITDA etc. 'Class' is the target variable, where 0 means didnot get bankrupt and 1 means got bankrupt. There are 42627 rows.

## Steps:
1. Read and merge the data. There are 5 csv files, each representing one financial year.
2. Handle missing values.
    - Missing values are entered as '?' and these features are read as object dtype, when infact they are float type.
    - They are replaced with NaN and changed the features as float type.
    - Impute them with median of the values as we have outliers.
    
3. Handle outliers.
    - A custom function, get_outliers_Zscore is used to collect the outliers with a threshold of 3.
    - It is observed that every column has outliers.
    - Ids of these outlier records are stored in a list.
    - Distribution of values in each attributes are smoother after removing the outliers.
    - Applying transformations will futher normalize the distribution.
    
4. Perform Scaling
    - 3 Different types of scaling methods are used.
        - MinMaxScaler - Uses minimum and maximum of the series.
        - StandardScaler - Uses mean and zscore of the series.
        - PowerTransformer - Parametric and Monotonic transformations, useful when heteroscedasticity is present.
        
5. Multicollinearity
    - Varience inflation factor (vif) is used to find the corellated features and drop them.
    
6. Modeling
    - A dataframe is used to collect all the expermients. (MLFlow can also be used).
    - Grid search is used to find the best parameters for XGBoost.
    - Different combinations of parameters and scaling is experimented.
    
## Results:
    - XGBoost with PowerTransformer gave the best results.
        - Train F1 score: 0.89 and Test F1 score: 0.74
Citation Request:

Zieba, M., Tomczak, S. K., &Tomczak, J. M. (2016). Ensemble Boosted Trees with Synthetic Features Generation in Application to Bankruptcy Prediction. Expert Systems with Applications. [Web Link]

BibTeX:
@article{zikeba2016ensemble,
title={Ensemble Boosted Trees with Synthetic Features Generation in Application to Bankruptcy Prediction},
author={Zi{k{e}}ba, Maciej and Tomczak, Sebastian K and Tomczak, Jakub M},
journal={Expert Systems with Applications},
year={2016},
publisher={Elsevier}
}