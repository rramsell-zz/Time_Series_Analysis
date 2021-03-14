# Time_Series_Analysis

Research Question
	What is the forecasted revenue for the next ten days? 
It will be beneficial to know how much revenue to plan on for budget cuts and strategic marketing. If the company has a better idea of how much revenue to expect, then every dollar can be accounted for and planned.

Objectives and Goals
	The goals of the research project are to answer the above research question using python. Furthermore, to offer valuable insight via modelling via explanatory analysis. How these goals will be accomplished are through the following means: time series visualization for trend analysis, data transformation to stationary for model fitting, train test splitting the data (with a 20% sampling method, industry standard), fitting a model, and forecasting the above question of ten days of revenue. The steps above will help to ensure the useability of the data for the company in predicting future revenues. This will allow for telecom to plan for every dollar and bolster strategic management initiatives within the company appropriately.
Summary of Assumptions
	Each model that is used in machine learning has certain assumptions. Time series modelling requires that data be stationary as well as no autocorrelation. For the data to qualify as stationary, it must lack trends (cyclical or seasonal). Furthermore, if the data is not centered around zero in its stationary plot some manipulation must happen. Namely, the model must have constant value “C” added to the model’s creation function. Autocorrelation is the statistical insignificance found between variables in timestep t and t-1. If autocorrelation exists, the model is including insignificant, even irrelevant, data and may be overfitting.
  
Time Step Formatting
  This time series can be viewed several ways. Split as many times ‘n’ into the whole time series ‘y’. However, split evenly (as well as at the start of a new local minimum and maximum) it follows that there are nine time-steps in the data. About every 81.22 days.  The data cannot be split into non-integer types for modeling, so the series can either be viewed as having too many data entries, or too few. 
  
Stationary
	Stationary data simply means data which contains no trends or autocorrelation. It also happens to be a requirement of the data to fit it to a model. There are a few tests and metrics which provide insight into a dataset’s trends. One way is to plot the time series realization and visually assess for trends. The second way is to perform a Dicky Fuller test on the data which will provide a metric for comparison. In this project both will be performed for confidence in the analysis. 
Visual Assessment
	It is apparent that there are cyclical trends throughout the data. Seasonality can be ruled out as it does not have a 365 seasonal trend for local minimums and maximums. 
Dickey Fuller Test
	The first item returned (in the 0th position), is a test statistic. The more negative the value returned by this test, the more likely the data is stationary. The second value is the p-value. When the p-value is small, we reject he null hypothesis and reject that the data is non-stationary.  The results of this test provide insight into the high possibility of trend within the data. Furthermore, the need for data transformation. 
  
Steps to Prepare the Data
	There were several necessary steps for the data to be modelled. Those steps being:
1.	Import the packages necessary for the project.
2.	Read the CSV file and assign the dataset to a variable.
3.	Display various statistical properties of the data to assess it visually and programmatically for outliers, nonsensical entries, and null values. Dimensions, data type, distributions and the first five features of the dataset were analyzed.
4.	Plot the realization of the time series.
5.	Plot the Autocorrelation and Partial Autocorrelation functions to check for model type.
6.	Plot Power Spectral Density to further assess model needs.
7.	Perform the Dickey Fuller test on the data.
8.	Use the difference of squares method to transform the data to stationary.
9.	Perform a second Dickey Fuller test on the transformed data.
10.	Perform a train test split with a sample size of 20%.
These steps, once performed, allowed for the time series modelling to take place.


Report Findings and Visualizations
	The insights gained through the project are organized chronologically in the below sections. These sections also contain accompanying visualizations where appropriate. 
The Presence or Lack of a Seasonal Component 
Seasonal trends are defined as a change in local related local minimums and maximums and trend as they correlated to a season. The perfect example is with the beginning of summer: ice cream sales climb and hot chocolate sales drop. Seasonality can be visually assessed on a 365 day, or 12-month, time-step in mind. Above, the visual revenue is plotted by day. There are obvious trends within the visual, but more so cyclical than seasonal. Therefore, the data has a definite lack of seasonality.

Trends
	The data contains trend. This is proven via the Dickey Fuller test and visually via pyplot. Below is the screenshot associated with the statistical test proving cyclical trends, above is the visualization for cyclical trend activity.
	The first and second metric returned by this test proves trend. The lower the negative number for the 0th position, the more stationary. The smaller the second metric (p-value) the more we can reject the null hypothesis and non-stationary type.
Autocorrelation Function
	Autocorrelation as described in previous sections is the presence of statistically insignificant data as it pertains to time-step t-1. The autocorrelation function proves the type of function which will best fit the time series model. Below are the two graphs and screenshot of the autocorrelation function as they show variance with respect to position t-1.
  Another important correlation function is the partial correlation function provided by tsaplots.

The Decomposed Time Series
To decompose a time series dataset, one must simply transform the data to remove trend and autocorrelation. The method used is the difference of squares. Below is a screenshot of the code used and the visualization of the transformed data.

Confirmation of the Lack of Trends in the Residuals of the Decomposed Series
	Visually, the data appears to be trendless. However, another Dickey Fuller test can be performed to statistically test the decomposed series for trend. Here is a screenshot of the code and findings of the Fuller test on the transformed data. The p-value is 0.0 allowing for a rejection of the null hypothesis and a rejection of non-stationary claim in the data. In layman’s terms, the data lacks trend and is ready for a model. Also, the first metric returned by the test is far more negative than the last which further justifies the lack of trend. These two assessments, visual and Fuller test, confirm the lack of trends in the decomposed series.
  
Arima Model
	The model is ARIMA(2, 1, 2). The model’s statistical summary is provided in the ipynb file.
	The mean squared error test provides insight into the model’s accuracy with a low score of .496. This is a great indication of model performance. Furthermore, the steps of decomposition are justified by the Dickey Fuller test and the autocorrelation functions.
 
Forecasting Using Arima Model
	The above model was used to forecast the next 10 time-steps. Below is the snapshot of the code and its output. It is important to remember that the farther out a prediction, the more unstable it becomes. Also, that models must be updated to maintain their accuracy in prediction.
 
Output and Calculations
	Many calculations were performed in this analysis. The calculations will be broken into steps in this section and a summary provided for each. Further, code and outputs will be provided throughout the section.
  1.	Dimension, distribution, data type, and visual inspections were performed. This was to assess the data for cleanliness and tidiness. These steps help the analyst to better understand the data being worked with and ensure a more accurate model. These calculations help with outlier and null value imputation as well as providing realistic expectations for forecasting.
  2.	Visual inspection of trends. If there are trends in the data, they need to be made stationary to fit to any time series model. 
  3.	Autocorrelation and partial autocorrelation functions. This shows statistical significance between point t and t-1. The lesser the significance, the less useful the data is to our model. Also, it can lead to overfitting if not checked.
  4.	Spectral Density Analysis. This helps to know the dimensional space ‘k’ observed throughout the data in the time series. It uses a signal to mathematically and graphically visualize this.
  5.	Dickey Fuller Test. This test provides several metrics for series evaluation. The first metric returned is a statistical test. The more negative, the less trend exists in the series. The second is the p-value. The closer the p-value is to 0, the more we reject the null hypothesis and reject non-stationarity. In summary, this test allows the analyst to perceive how many transformations need to happen to the series to fit it to a model. It also helps prevent overfitting.
  6.	Visualization of stationary decomposed series. This is a visual check to ensure lack of trend in the series. 
  7.	Second Dickey Fuller test. This test is performed again to ensure the transformation had the desired affect on the series. 
  8.	Train test split, visualization, and mean squared error test. The train test split is commonplace in model engineering to create a learning capability for the machine. A 20% sampling method was used (as is standard). With an ARIMA model with the order of 2, 1, 2, was used according to the results of the Dickey Fuller test and the predictions were graphed alongside the residual actuals.
  9.	Model statistical summary. This is used to find the model’s accuracy, utility, and coefficients. 
  10.	Predicted mean forecast. The model was used to forecast ten time-steps ahead of the series. It should be noted that the farther one forecasts, the less accurate the forecast becomes. This is useful to the company as it provides insight into future cash flows so every dollar can be planned. Strategic management initiatives ought to use this forecast to act instead of being acted upon.
 
Results
	The results of the analysis answer the research question posed initially. That being, “What is the forecasted revenue for the next ten days?” An ARIMA model has been selected, the prediction interval of the forecast determined, forecasts were made, and the model has been evaluated with error metrics. 
  
Selection of an ARIMA Model
	The selection of the ARIMA model was done via the Dickey Fuller test and Autocorrelation Function. These tests provided a decomposition transformation of one step. The model’s order was determined and a train test split with 20% sampling was performed. 
  
The Prediction Interval of the Forecast
	The prediction interval of the forecast was determined largely by the mean squared error test on the model. Through several iterations of forecasts, the current model had the lowest RSE of .46.

Justification of Forecast Length	
With all forecasting models, the farther the forecast goes into its prediction, the less accurate it becomes. This is due to a lack of support of current data. This is remedied by the constant updating of model input data which ensures model viability. With time series modelling, the farther the data is forecast, the more unstable it becomes and it flatlines. In the forecast visualization above you can see the data tapering at five time-steps. This is the justification for the length of the forecast. Any longer and the information becomes useless to the user. 

Model Evaluation Procedure and Error Metric
	The model was evaluated four ways and with three metrics. Visually the predictions were plotted with the actuals to determine model accuracy. Via metric the model was evaluated using: the mean squared error, AIC, and BIC. The mean squared error for the model was .46 which is extremely low. The AIC and BIC metrics are measurements of statistical significance between model in time t. Below is a screenshot of the predictions vs actuals graph, AIC, BIC, and MSE scores.

Recommendations
	The astounding accuracy of the model in comparison to actuals lead us to actionable insights. First, we know we can claim insight from our revenue data (hence the project). Second, we know we have an accurate ARIMA model that is accurately forecasting our data for 10 time-steps. Third, there is a downward trend over the next 10 days in revenue. Thus, the conclusion of this syllogism is depending on the unknown variable of need within the company. 
	The recommendation is to either increase marketing and possibly effect our top line or cut expenses and decrease the bottom line. Either way, strategic management initiatives should plan for each dollar as the model says it will be available. 
	According to the forecast, the company should expect to see a downward trend and drop of $200k in the next 10 days in revenue. Whether the executive team decides to focus on top or bottom line, something must be done to derail this trend and send revenue in a positive direction. As changes are made and strategic management initiatives are implemented, the model should be updated daily to account for changes in the supporting data. The model will become increasingly less accurate the farther it gets from day 731. 
