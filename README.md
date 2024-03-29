# Capstone-project

## Research Objective/ Challenge:
The research objective is to establish the real-time reactor powder Melt Flow Index (MI) prediction model  based on important factors provided using a python program and achieve an above 80% average accuracy.

Importance of challenge:
By building this more precise model, the team hopes to replace traditional tester, which is to test the Powder MI every four hours manually to ensure that it is within the acceptable range. By solving the challenge, the optimized model will reduce the production cost, optimize manufacturing, and prevent wasteful production. Introducing the automation process will simplify the production cycle, reduce labor cost, and better utilize production capacity. In the long run, by applying the automation process that no other competitors has to all production lines, Formosa Plastics would be able to improve production volumes and achieve sustainable growth with the unique competitive advantage.

Research Questions and Hypotheses:
Research Question: What ingredient factors from given input factors predict whether the Powder MI value will stay in the acceptable range, and how can these factors be used to build an AI model with an accuracy above 80%?
Hypotheses: Different input factors and most fitted models will be applied when predicting the Powder MI value based on the prograde types.

## Data Overview

Datasets Introduction:
The “MI QC data” includes the Powder MI value for each 4-hour interval and the product grade (product type) for every 1-minute interval. The tester measures the Powder MI every 4 hours.
The “Tag Data” has the observation time and material quantities of the production for each 1-minute interval.

Datasets Quality Issues:
When the team receives the two datasets, several data quality issues are identified. First, only 0.2% of the data have MI values, which means only 0.2% of the data can be used as training data to the model. Using 0.2% data with MI values to predict the MI values of the rest 99.8% data will affect the accuracy of the result. The number of MI values may be not enough to train and accurately predict the fitted MI. The missing interpretation of factors also impedes the understanding of the project and objective.

## METHODOLOGIES

Data Cleaning:
The two datasets have a common column “time”, in which time of product grade in “MI QC data” can be related to that in the “Tag data” and the time of Powder MI is lagged back by 105 minutes since the Powder MI value reflects the status of 105 minutes ago. Therefore, the team subtract 105 minutes from the time of Powder MI.
With the help of Excel vlookup function, the group left join the product grade and MI value of “MI QC data” with “Tag data” by time, by which the data clearly reflects what product was producing and what was the MI value for that. Now the new data has both predictor and the variables required for model building. Besides, there are rows that lack material variables. Since most of the variables are lost in those rows and the number of rows with missing value is a few, the team omit those rows to ensure that our dataset is without missing variables.

Data Mining:
Starting with the bar chart of the powder MI, the team plots the average of Powder MI as the first step of data mining. The means of MI is different for various product prograde. This is also why the group raise the hypothesis, which applying different factors and models to ensure receiving highest accuracy rate. A sample heatmap listing below pairs the first 18 factors and the powder MI in 2-dimensional form. It provides a colored visual summary of the correlation between each factor. The light yellow represents low correlation and strong red/ green color represents high correlation. The factors with correlation below 0.1 will be drop with manually when choose factors. Then, by graphing the time series chart, a usual spike on 11/10/2018, 19:45 is shown. It is considered as outlier for now and still need more investigation for the next step.

## Data Modeling:
Our group has tried different models, including Linear Regression, Random Forest, Gradient Boosting, Bagging, XGboost, and Voting Regressor. At the same time, different variable combinations were tried, including variables selected by correlation analysis, variables selected by feature selection, all sets of variables, etc. We evaluated the quality of a model in two means, one is the RMSE (the measure of the differences between values predicted and the values observed); the other one is accuracy (For the accuracy criteria of over 80%, after consulting with the client, it is defined in two ways, the first acceptable definition is that 80% of the predicted data is 20% above and below the observed value; the second one is that 80% of the predicted value is +1 or -1 compared with the observed value). Table 2.3 lists all of the models we tried as well as their RMSE and the accuracy in two means.
Based on the result, we found that the Gradient Boosting Model (GBM) with all variables performs the best, with the lowest RMSE and the highest accuracy in both means.
Besides the RMSE and accuracy, there are two advantages that make this GBM the best. The first is that GBM is robust to overfitting. Using large number of rows of data may cause the problem of overfitting, resulting in a large error when being applied and away from the train data. Since GBM is robust to overfitting, it can more accurately and stably predict the MI value. The second advantage is that GBM model can process data faster and easier, which can reduce unnecessary computing burden and latency so that our client can easily access to the model.
