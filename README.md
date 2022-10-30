# Cryptocurrencies

## Overview 
Martha is a senior manager for the Advisory Services Team at Accountability Accounting, one of the most important clients. Accountability Accounting, a prominent investment bank, is interested in offering a new cryptocurrency investment portfolio for its customers. The company is not familiar with cryptocurrencies so we will create a report that includes what cryptocurrencies are on the trading market and how they could be grouped to create a classification system for this new investment. The data is not ideal to work with, so it will need to be processed to fit the machine learning models. Since there is no known output for what Martha is looking for, unsupervised learning will be used. A clustering algorithm will be used to group the cryptocurrencies and data visualizations will be used to share the findings with the board.

## Resources
### Software
- Python 3.7.13
- Conda 22.9.0
- Jupyter Notebook

### Data Source 
-  [crypto_data]() csv file from [CryptoCompare](https://min-api.cryptocompare.com/data/all/coinlist)

## Results
### Deliverable 1: Preprocessing the Data for PCA 
Using Pandas, the dataset will be preprocess in order to perform PCA in Deliverable 2. The completed crypto_clustering Jupyter Notebook can be referenced [here]().

1. The following five preprocessing steps have been performed on the crypto_df DataFrame:
    - All cryptocurrencies that are not being traded are removed:
    - The `IsTrading` column is dropped:
    - All the rows that have at least one null value are removed:
    - All the rows that do not have coins being mined are removed:
    - The `CoinName` column is dropped:
    
2. A new DataFrame is created that stores all cryptocurrency names from the `CoinName` column and retains the index from the `crypto_df` DataFrame:

3. The `get_dummies()` method is used to create variables for the text features, which are then stored in a new DataFrame, `X`:

4. The features from the `X` DataFrame have been standardized using the StandardScaler `fit_transform()` function:


### Deliverable 2: Reducing Data Dimensions Using PCA
Using the Principal Component Analysis (PCA) algorithm, the dimensions of the `X` DataFrame will be reduced to three principal components and these dimensions will be placed in a new DataFrame.

1. The PCA algorithm reduces the dimensions of the `X` DataFrame down to three principal components:

2. The `pcs_df` DataFrame is created and has the following three columns, `PC 1`, `PC 2`, and `PC 3`, and has the index from the `crypto_df` DataFrame:


### Deliverable 3: Clustering Cryptocurrencies Using K-means
Using the K-means algorithm, an elbow curve will be created using `hvPlot` to find the best value for K from the `pcs_df` DataFrame created in Deliverable 2. Then, the K-means algorithm will be run to predict the K clusters for the cryptocurrencies’ data.

1. The K-means algorithm is used to cluster the cryptocurrencies using the PCA data, where the following steps have been completed:
    - An elbow curve is created using `hvPlot` to find the best value for K:
    - Predictions are made on the K clusters of the cryptocurrencies’ data:
    - A new DataFrame is created with the same index as the `crypto_df` DataFrame and has the following columns: `Algorithm`, `ProofType`, `TotalCoinsMined`, `TotalCoinSupply`, `PC 1`, `PC 2`, `PC 3`, `CoinName`, and `Class`:


### Deliverable 4: Visualizing Cryptocurrencies Results
Using Plotly Express and `hvplot` to create scatter plots, the distinct groups that correspond to the three principal components created in Deliverable 2 will be visualized, then a table with all the currently tradable cryptocurrencies will be created using the `hvplot.table()` function.

1. The clusters are plotted using a 3D scatter plot, and each data point shows the CoinName and Algorithm on hover:

2. A table with tradable cryptocurrencies is created using the `hvplot.table()` function:

3. The total number of tradable cryptocurrencies is printed:

4. A DataFrame is created that contains the `clustered_df` DataFrame index, the scaled data, and the `CoinName` and `Class columns`:

5. A `hvplot` scatter plot is created where the X-axis is "TotalCoinsMined", the Y-axis is "TotalCoinSupply", the data is ordered by "Class", and it shows the CoinName when you hover over the data point:



## Summary
The purpose of this analysis was to utilize unsupervised learning to process and cluster data, reduce dimensions, and reduce principal components using PCA is order to present the analysis to clients preparing to get into the cryptocurrency market.
