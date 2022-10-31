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

1. The following five preprocessing steps have been performed on the `crypto_df` DataFrame:
    - All cryptocurrencies that are not being traded are removed: <br /> ![image](https://user-images.githubusercontent.com/108038989/198919822-9abf2471-ae70-46ef-a03d-8a8a2b1f2925.png)
    - The `IsTrading` column is dropped: <br /> ![image](https://user-images.githubusercontent.com/108038989/198919914-be586ae8-cf4c-4cfd-8138-89ffcc4012c5.png) 
    - All the rows that have at least one null value are removed: <br /> ![image](https://user-images.githubusercontent.com/108038989/198919972-0ed12396-d1a2-4cbf-8020-8d005169dd8e.png)
    - All the rows that do not have coins being mined are removed: <br /> ![image](https://user-images.githubusercontent.com/108038989/198920020-b2f782ed-3641-4cf1-9024-4b6536b7af3b.png)
    - The `CoinName` column is dropped: <br /> ![image](https://user-images.githubusercontent.com/108038989/198920096-ccae2ef3-c32e-4169-aaf8-ce38350b72da.png)
    
2. A new DataFrame is created that stores all cryptocurrency names from the `CoinName` column and retains the index from the `crypto_df` DataFrame: <br /> ![image](https://user-images.githubusercontent.com/108038989/198920183-b1d28a81-aa2c-42bb-8fb8-5dde529b82ca.png)

3. The `get_dummies()` method is used to create variables for the text features, which are then stored in a new DataFrame, `X`: <br /> ![image](https://user-images.githubusercontent.com/108038989/198920228-f49e7dac-1952-4ebb-8dfe-ca12adf7e16d.png)

4. The features from the `X` DataFrame have been standardized using the StandardScaler `fit_transform()` function: <br /> ![image](https://user-images.githubusercontent.com/108038989/198920279-5a892b8b-2e39-4281-8839-ca1e811eb0f3.png)

### Deliverable 2: Reducing Data Dimensions Using PCA
Using the Principal Component Analysis (PCA) algorithm, the dimensions of the `X` DataFrame will be reduced to three principal components and these dimensions will be placed in a new DataFrame.

1. The PCA algorithm reduces the dimensions of the `X` DataFrame down to three principal components: <br /> ![image](https://user-images.githubusercontent.com/108038989/198921597-8a802f9e-f7f8-4c3e-b678-7ced2a5df22a.png)

2. The `pcs_df` DataFrame is created and has the following three columns, `PC 1`, `PC 2`, and `PC 3`, and has the index from the `crypto_df` DataFrame: <br /> ![image](https://user-images.githubusercontent.com/108038989/198921640-9d30985f-33e0-4ea2-b567-a2b4da425a83.png)

### Deliverable 3: Clustering Cryptocurrencies Using K-means
Using the K-means algorithm, an elbow curve will be created using `hvPlot` to find the best value for K from the `pcs_df` DataFrame created in Deliverable 2. Then, the K-means algorithm will be run to predict the K clusters for the cryptocurrencies’ data.

1. The K-means algorithm is used to cluster the cryptocurrencies using the PCA data, where the following steps have been completed:
    - An elbow curve is created using `hvPlot` to find the best value for K: <br /> ![image](https://user-images.githubusercontent.com/108038989/198923239-1a4db9f5-280e-4ed1-9a93-6fbdb67572e3.png)
    - Predictions are made on the K clusters of the cryptocurrencies’ data: <br /> ![image](https://user-images.githubusercontent.com/108038989/198925788-3f3dc789-e42b-4fa6-83b1-89cb0f437a94.png)
    - A new DataFrame is created with the same index as the `crypto_df` DataFrame and has the following columns: `Algorithm`, `ProofType`, `TotalCoinsMined`, `TotalCoinSupply`, `PC 1`, `PC 2`, `PC 3`, `CoinName`, and `Class`: <br /> ![image](https://user-images.githubusercontent.com/108038989/198925830-6e676cd0-431f-4b8e-9dee-d62cb607abb2.png)

### Deliverable 4: Visualizing Cryptocurrencies Results
Using Plotly Express and `hvplot` to create scatter plots, the distinct groups that correspond to the three principal components created in Deliverable 2 will be visualized, then a table with all the currently tradable cryptocurrencies will be created using the `hvplot.table()` function.

1. The clusters are plotted using a 3D scatter plot, and each data point shows the CoinName and Algorithm on hover: <br /> ![image](https://user-images.githubusercontent.com/108038989/198927212-85f2590b-204f-4d2f-8bb6-e9df55765eed.png)

2. A table with tradable cryptocurrencies is created using the `hvplot.table()` function: <br /> ![image](https://user-images.githubusercontent.com/108038989/198927291-d28a6753-6fdb-408e-9c13-836a1732376e.png)

3. The total number of tradable cryptocurrencies is printed: <br /> ![image](https://user-images.githubusercontent.com/108038989/198927660-d615fb18-fdda-4ff4-9ee5-d5201045d943.png)

4. A DataFrame is created that contains the `clustered_df` DataFrame index, the scaled data, and the `CoinName` and `Class columns`: <br /> ![image](https://user-images.githubusercontent.com/108038989/198929065-4ff81f54-746d-4741-ae85-9d329bf597a1.png)

5. A `hvplot` scatter plot is created where the X-axis is "TotalCoinsMined", the Y-axis is "TotalCoinSupply", the data is ordered by "Class", and it shows the CoinName when you hover over the data point: <br /> ![image](https://user-images.githubusercontent.com/108038989/198929415-fc494375-394d-42ab-a6af-f05ef2929762.png)

## Summary
The purpose of this analysis was to utilize unsupervised learning to process and cluster data, reduce dimensions, and reduce principal components using PCA is order to present the analysis to clients preparing to get into the cryptocurrency market.
