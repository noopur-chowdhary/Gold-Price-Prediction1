


<img width="1536" height="1024" alt="Gold_price+pred" src="https://github.com/user-attachments/assets/939c5a5c-25e3-45c9-8aa5-575a5b8dddf4" />




**Project Overview**

This project focuses on predicting gold prices using multiple machine learning and deep learning models.
The objective is to compare the performance of classical regression models, ensemble methods, and LSTM networks on structured financial time-series data.

Models used in this project:

Lasso Regression (with GridSearchCV)

Random Forest Regressor

XGBoost Regressor

LSTM (Long Short-Term Memory)

The comparison is based on error metrics such as MAE, MSE, RMSE, and R² score.

**Data Cleaning and Preprocessing**

The dataset contains gold price along with related financial indicators.
Before training the models, several preprocessing steps were performed to ensure data quality and consistency.

Missing values were handled using mean imputation.
Redundant features were removed to reduce multicollinearity, including dropping the SLV column.
Outliers were detected using the IQR method and removed to avoid distortion in model training.
The data was then normalized using StandardScaler to ensure all features are on the same scale, which is especially important for regularized regression and neural networks.

A correlation matrix was also computed to understand the relationships between variables and to verify that the selected features were relevant for prediction.


**Feature Engineering**

To capture short-term trends in gold prices, rolling statistics were applied.
A rolling mean with window size 3 was used to smooth the price series and reduce noise.

Skewness of the features was analyzed to understand distribution characteristics.
This helped verify that scaling and outlier removal were necessary.

For the LSTM model, the dataset was transformed into sequential format by creating fixed-length input sequences.
This allowed the neural network to learn temporal dependencies in the data.



**Models**
Lasso Regression

Lasso regression was used as a baseline regularized linear model.
Hyperparameters were tuned using GridSearchCV to find the optimal regularization strength.
This model helps reduce overfitting and performs feature selection automatically.

Random Forest Regressor

Random Forest was used as a non-linear ensemble model capable of capturing complex relationships between features.
It performs well on structured tabular datasets and is robust to noise and outliers.

XGBoost Regressor

XGBoost was used as a gradient boosting model.
It is known to provide strong performance on financial and tabular datasets due to its ability to model nonlinear feature interactions efficiently.

Among the classical machine learning models, XGBoost produced the lowest prediction error.

LSTM Model

An LSTM network was implemented to model the time-series nature of gold prices.
The data was converted into sequences, and the network was trained using past observations to predict future values.

The model consisted of stacked LSTM layers followed by a dense output layer.
Performance was evaluated using the same metrics as the other models.


**Model Evaluation**

All models were compared using:

Mean Absolute Error (MAE)

Mean Squared Error (MSE)

Root Mean Squared Error (RMSE)

R² Score

A grouped bar chart was plotted to visualize the error values for:

Lasso

Random Forest

XGBoost

This comparison showed that XGBoost achieved the best performance among the machine learning models.

The LSTM model was evaluated separately using the same metrics.


**Discussion**

Gold prices are recorded over time and may exhibit temporal dependency,the problem naturally has a time-series structure.
Because of this, we expected the LSTM model to be the best performer, as LSTM networks are specifically designed to learn temporal dependencies in sequential data. In theory, a deep learning model that can capture patterns across time steps should outperform classical machine learning models on such data.

However, the results were against this intuition.
The experiments showed that XGBoost and Random Forest achieved lower prediction error than the LSTM model. This behavior can be explained by the characteristics of the dataset and the nature of the problem.

First, the dataset used in this project is relatively small. LSTM networks generally require large amounts of sequential data to learn stable temporal patterns, while tree-based models such as Random Forest and XGBoost perform well even with limited data. With only a few thousand observations, the LSTM model does not get enough information to fully utilize its sequential learning capability.

Second, the gold price in this dataset depends strongly on multiple financial indicators such as stock index values, oil prices, and other related variables. This makes the problem closer to a multivariate regression task rather than a pure time-series forecasting problem. Tree-based ensemble models are very effective at learning relationships between features, which gives them an advantage over LSTM in this case.

Third, the dataset is structured and well-behaved, with clear correlations between variables. XGBoost is known to perform exceptionally well on structured tabular datasets, which explains why it achieved the best performance among all models.


**Conclusion**

This project demonstrates that model performance depends on the nature of the dataset.

Lasso provides a simple regularized baseline.

Random Forest captures nonlinear relationships effectively.

XGBoost gives the best performance for structured financial data.

LSTM works for sequential modeling but may not outperform ensemble methods on small noisy datasets.

The results highlight that deep learning is not always superior, and model selection should depend on the data characteristics.
