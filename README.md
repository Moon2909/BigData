# Bigdata
**Detecting real-time anomalies in stock time series data**

Ho Thanh Duy Khanh†, Nguyen Thi Nguyet†, Nguyen Thanh Nhan† and Nguyen Thi Phuong Thao†

**†** VNUHCM - University of Information Technology, Viet Nam.

Contributing authors: [20521445, 20521689, 20521701, 20521936]@gm.uit.edu.vn

## Abstract
Detecting real-time anomalies in stock time series data poses a significant challenge in the financial domain due to the unavailability of labeled data for identifying trading anomalies or stock price movements. This study introduces a real-time anomaly detection system for stock data from Apple Inc., collected over five weeks using a financial API,  recording minute-level stock price information during trading hours. Un- supervised anomaly detection models, including Isolation Forest, Spectral Residual, Local Outlier Factor, Random Cut Forest, and Luminol,  are employed to create label functions for each data point. We construct  a weakly supervised learning model based on the composite label functions to provide weak labels. Subsequently, we train a classification model  using LightGBM and evaluate five basic machine learning models (SVM, XGBoost, KNN, Random Forest, Gradient Boosting Machine) to detect anomalies in the data. The results show that data balancing through  Synthetic Minority Oversampling Technique (SMOTE) significantly improves the anomaly detection capability, particularly for the Random  Forest model. For the online component, real-time data is collected from  the Binance platform and processed through Kafka and Spark Streaming. The trained offline model is then utilized to predict anomalies in the  streaming data. The proposed system offers a comprehensive approach to real-time anomaly detection in stock data, providing crucial support for investors and financial experts in making timely and informed decisions. 

## 1. Pipeline
To tackle this challenge, our research introduces a real-time anomaly detection system, which consists of two main components:  
1. **Offline**: In this component, we develop and train an anomaly detection model using historical data with labeled anomalies. This offline model serves as the foundation for identifying abnormal patterns and establishing the basis for anomaly detection.
2. **Online**: The second component involves the implementation of a real-time anomaly detection system. This system is designed to continuously process incoming data in real time, making it capable of detecting anomalies as they occur in livestock time series data. (Observe Fig.1)

![PipelineOnline](https://github.com/Moon2909/Bigdata/blob/main/PipelineOnline.png)

## 2. Dataset
### 2.1. Collect Data
We collected the stock price data of Apple (stock symbol: AAPL) within the timeframe from June 12, 2023, to July 14, 2023 (5 weeks) using a financial API. The data was collected at a 1-minute frequency (interval='1min') and only  during trading hours, from 4:00 AM to 7:59 PM. No data was collected on non-trading days, such as Saturdays and Sundays.  
Through the financial API, we obtained 21,972 rows of data with 6 columns, providing detailed information about the real-time trading timestamps, opening price, highest price, lowest price, closing price, and trading volume of the Apple  stock in each trading session. This data was delivered with accuracy and real-time precision, enabling us to capture significant fluctuations and patterns in  Apple’s stock price during the research period. 

### 2.2. Preprocessing data
Furthermore, to address the issue of missing data points, we employed two prominent data imputation methods, namely the **Linear Interpolation** and **Effective Dynamic Time Warping Based Imputation** techniques, as referenced in the scholarly work titled [**"An Empirical Study of Imputation Methods for Univariate Time Series"**](https://www.researchgate.net/publication/351095422_An_Empirical_Study_of_Imputation_Methods_for_Univariate_Time_Series_SO_SANH_MOT_SO_PHUONG_PHAP_XU_LY_DU_LIEU_THIEU_CHO_CHUOI_DU_LIEU_THOI_GIAN_MOT_CHIEU). These methods were skillfully applied to the collected Apple stock price dataset, which exhibited varying degrees of missing values on different dates.

![ResultPreprocessing](https://github.com/Moon2909/BigData/blob/ResultPreprocessing.png)

Based on the imputation results mentioned in Table 1, Linear Interpolation yielded more favorable outcomes than the eDTWBI method across various levels of missing data. Consequently, this method closely approximates reality and proves to be more effective in reconstructing real-time temporal data for the Apple stock price dataset. Building upon this foundation, we have made the decision to employ the Linear Interpolation method for filling in the missing data points in the minute-level stock price dataset. Following the data preprocessing, we obtained a dataset with 24,000 samples and 6 features. 

### 2.3. Labeling data
In the absence of labeled anomaly data, we employed a well-defined pipeline outlined in the scholarly work titled [**"Label-Efficient Interactive Time-Series Anomaly Detection"**](https://arxiv.org/abs/2212.14621) to construct a sophisticated model capable of effectively detecting anomalies within the stock price data of Apple. 

## 3. Models
We utilized five fundamental binary classification models in our approach: Support Vector Machine, eXtreme Gradient Boosting, Random Forest, K-nearest neighbors, and Gradient Boosting Machine.

## 4. Results
![Result](https://github.com/Moon2909/Bigdata/blob/main/Result.png)

