---
title: "Airline Delay Prediction Report for American Airlines"
author: "Logistics Transport Aviation"
date: "03/10/2021"
output:
  html_document:
    toc: yes
    toc_float: yes
    toc_depth: 3
    fig_caption: yes
  pdf_document:
    toc: yes
    toc_depth: '3'
  word_document:
    toc: yes
    toc_depth: '3'
subtitle: STDS - AT2
---
  


# Introduction

Aircraft delays have serious economic impacts that represent a logistical headache for airlines, airports, airline crew, and passengers alike. In a 2010 study by the National Center of Excellence For Aviation Operations Research, an estimated 31.2 billion US dollars was lost due to direct and indirect costs of airline delays in the United States for 2007. These expenses included maintenance costs, extra paid hours for flight crew, the extra use of fuel, and airport fees. As an example, airlines have dedicated time slots at airport gates and unexpected delays exceeding the expected time slot can cost thousands of dollars by the minute. 
Many factors can contribute to aircraft delays. These may include unavoidable reasons such as inclement weather, unforeseen aircraft mechanical breakdowns, or a multitude of passenger-related incidents. Airline delays then create complicated scenarios for airline schedulers as a delay for one aircraft may impact the flight schedule for all consecutive flights using that aircraft. Passengers with connecting flights may need to be ticketed on other flights, the reserve flight crew may need to be called if the current flight crew exceeds their flight hours, or delays may continue to have a snowball effect on later flights causing them to also be delayed (Ball, 2010).
Thus, understanding the impact of these variables on aircraft on-time performance can help elucidate ways and methods to mitigate these airline delays. By doing so, steps can be made to reduce airline costs associated with these delays, benefiting the airlines' stakeholders. 
The airline industry has presented losses in the amount of billions of dollars per quarter since the COVID pandemic impacted the world. According to American Airlines newsroom (2021), this Airline had a $1.3B operating loss during the first quarter of 2021 alone, major competitors such as Delta Airlines and United Airlines had similar results.

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/others/q1.png" width="671" />

Airlines are clearly going through a very difficult period, and even though it is not in their hands to solve all the current challenges since they are subject to decisions from governments and other entities, this situation also presents a good opportunity for companies like American Airlines to take action in certain areas like on-time performance and therefore improve their financial results. 
We have conducted exploratory analysis and linear regression models on airline delays utilizing data for domestic flights in the USA from January 2019 to March 2021. This decision was made to include pre-COVID and COVID data and also count Q1 results for 3 different years. We compared American Airlines to Delta and United Airlines, based on Brand value, Market value, and Domestic Market Share (Statista, 2021). 

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/others/mac.png" width="670" />

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/All Charts/On Time Bar.png" width="455" />
During the last couple of years around 30% of the domestic flights in the United States have presented some sort of delay. We can see that the 3 airlines present almost identical results, in terms of the proportion of delayed flights against the total number of flights. This shows us the big opportunity that the industry has. Especially taking into consideration that every minute of delay costs airlines around $74 dollars (Airlines for America, 2020). Just during 2020, American Airlines domestic flights reported over 4 million minutes in delays just in domestic flights, meaning an approximate $300 million dollars were lost for this reason. Even though our analysis focuses entirely on domestic flights, our results can be taken into consideration to improve on-time performance in International flights as well and have a greater impact on our financial results as well as our customer satisfaction indexes.

# Research Questions
## What are the main causes for Airline delays? (Variables that influence departure delays)

The question we want to answer with our linear regression model is a variation of this question: Which factors are most correlated to, and influence greatly, on-time aircraft performance?
 
<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/All Charts/Total minutes of delay for AA from 2019 to 2021.png" width="433" />

When looking at the main causes of delays for American Airlines flights between 2019 and 2021 we can see that the main reason corresponds to a late-arriving aircraft, meaning that a previous flight with the same aircraft presented an arrival delay causing the present flight to also depart late.  This is followed closely by the second reason, carrier delay. This delay can be attributed to circumstances within the airline's control such as maintenance or crew problems, aircraft cleaning, baggage loading, fueling, among others. National Aviation System (NAS) delays, weather, and security issues have a lower impact on the total amount of delays. Since the greatest proportion of aircraft delays, outside of a late incoming aircraft, are reasons within a carrier�s control, most delays may be attributed to the airline's operations and therefore we have a great opportunity to reduce costs and improve our results.

## 2.2 How is American Airlines on-time performance compared to our two main competitors?

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/All Charts/Q1 by airline.png" width="433" />

We found that all three airlines have improved their on-time performance from 2019 to 2021. United Airlines has improved its average delay time by almost 23% in just 2 years and Delta has kept a steady leadership on airtime performance. This displays a great opportunity to improve our on-time performance, reduce costs, and improve passenger satisfaction while also keeping up with our main competitors.

More details about both questions will be explored during our further EDA and Linear regression model.

# 3.0 Our datasets

BTS Dataset: Our main data set is a comprehensive one including 65 variables and over 12 million observations (January 2019 - March 2021). Each month was collected separately and merged together to form one large data set of 4GB. An API from the International Civil Aviation Organization (ICAO) was used to transmute airport codes to names and another look-up table to transmute airline codes to airlines.

Aircraft Dataset: Dataset built by scraping HTML data for each airline using the rvest package to obtain data about the airline�s fleet type, manufacturer, and age. This data set was merged with our main dataset using the aircraft tail number, 18% of the tail numbers were missing from the BTS data set and are excluded from the analysis.

Employee Dataset: This dataset contains information about the number of employees per month by airline and is merged into our BTS dataset to determine any relations between the number of employees and delays.

# 4.0 Exploratory Data Analysis (EDA).

Overall summary statistics were calculated and are included in the appendix. In addition, individual variables were explored with histograms for numeric variables, and relationships between some variables were explored with scatter plots.

Domestic flights in the United States started to substantially decrease in 2020, this can be explained due to the major worldwide outbreak of the COVID pandemic all around the world which shut down travel overall, and this impacted air travel, even though some parts of the world were affected since 2019 it was not until March 2020 that most countries, including the United States, started closing their borders and limiting interstate traveling. 


<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/All Charts/Basic EDA/Rplot.png" width="366" />
2019
<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/EDA Plots/2019_monthly_flights.png" width="542" />

When we look at the flight frequency of each month during 2019, we can see that October had the highest flight frequency at 154,486 followed by August at 154,390. The first two months of January and February have the lowest flight frequency at 140,109 (7.96%) and 128,239 (7.29%) respectively of the whole year. Overall, the frequency throughout the 2019 pre-Covid19 pandemic was relatively evenly distributed around 8% each month. 

2020
<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/EDA Plots/2020_monthly_flights.png" width="542" />

2020 had a completely different behaviour, the first two months January and February have the highest flight frequency of the year, opposite to what happened in 2019. From March, the number started decreasing due to the outbreak of the pandemic and the travel ban came into effect (Ghosh,2020). Usually, July is known as the busiest travel month of the year within the airline industry as there are all kinds of demands for air travel such as vacations, school holidays, and business travels (Maynard, 2015). From our 2020 plot, July is only the 4th least busy month of the year. 

While we already started exploring and analyzing our data, a further EDA is needed to find existing and non-existing correlations between variables and select those that are independent and use them in our prediction model. It is also important to understand what our data looks like, what it is telling us and what value and insights we can find in our variables.

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/Column EDA/DAY_OF_MONTH.jpeg" width="1225" />
One of the first insights we found was that around the second third of the month, most predominantly between days 10 and 13 are the most popular days to travel, while the beginning and end of the month are less popular, the first 5 and last 5 days of the month are all located at the bottom while days 10 to 20 (second third) are all at the top.

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/Column EDA/DAY_OF_WEEK.jpeg" width="1225" />

When analyzing days of the week we found that flights are pretty evenly distributed with all days except for Saturday taking between 14.22% and 14.92% of the flights. The most popular days for flights are Mondays, followed by Fridays and Thursdays. This makes perfect sense taking into consideration there are many weekend trips departing either Thursday or Friday and returning on Monday and those are also the most common days for business travel.

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/EDA Plots/aircraft_count.png" width="542" />

When looking at the aircraft manufacturers we found that American Airlines� fleet is mostly composed of Airbus planes followed by Boeings which are the top 2 manufacturers worldwide (Statista, 2020), on the other hand, both Delta and United prefer to use Boeing aircraft. In general Boeing aircraft perform 54.12% of the domestic flights while Airbus aircraft account for 38.37%. McDonnell Douglas aircraft have been excluded from our analysis as they are predominantly flown by Delta and have since been retired from their fleet. Embraer craft have also been excluded as they represent a tiny fraction of overall flights and are predominantly operated by regional carriers such as Republic or SkyWest.

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/EDA Plots/aircraft_model.png" width="542" />

The Airbus A320 series (319, 320, 321) was the most used model to perform domestic flights accounting for almost 39% between the three carriers followed by the Boeing 737 at around 37%. The ERJ, MD-80, and MD-90 series have been excluded per the manufacturer reasons stated above.

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/Column EDA/AGE.jpeg" width="1225" />
When looking at the aircraft age, the most popular ages lie between 20 and 22 years, followed by newer aircraft between 5 and 8 years of age. Aircraft over 30 years old are rarely used.

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/EDA Plots/model_age.png" width="542" />


<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/EDA Plots/delay_by_age.png" width="542" />

However American airlines tend to have delays around 6 years of age while compared to the competitors which have fewer clusters around younger aircraft. This may indicate differences in delay based on aircraft age. American Airlines tends to have a greater amount of younger aircraft that have delays.

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/EDA Plots/flight_time_by_age.png" width="542" />

With all airlines, we see that most delays occur with flight time sub-200 minutes. This may indicate that longer flights have a greater opportunity to make up for delay time in the air, or that delays are compounded with multiple short flights and opportunities to be delayed in or around airport traffic.

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/Column EDA/ORIGIN_STATE_ABR.jpeg" width="1225" />
<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/Column EDA/DEST_STATE_ABR.jpeg" width="1225" />


<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/All Charts/Map EDA.jpeg" width="640" />

Furthermore, as evidenced by the heat map of the USA, We noticed that most delays tend to be frequent in higher density states which include primary airline hubs. As evident in the previous figures, Texas tends to have the most delays.
The main origins and destinations are states where these airlines have hubs, the top 16 states containing all the hubs from the 3 main airlines represent almost 89% of air traffic and therefore most of the delays occur within these busy airports. For that reason, we first decided to focus on the busiest airports and subset our model. Finally, we made the decision to subset our model exclusively to California, since it was the second busiest state, contains a higher average departure delay, and all three airlines have a primary hub located here. This model will then be used to generalise on-time performance across other hub states.

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/EDA Plots/flight_delay_by_daytime_california.png" width="542" />

One interesting phenomenon we can observe from the graph is that flight delays increase as the day progresses. This shows that previous departure delays do affect subsequent departure delays on other flights or following flights. 
The gap between 00:00 and around 6:00 in the morning is due to airports� curfew time, where airports normally don't have flights departing and arriving during that time period. 

### 4.1.1 Metrics on data types
 


When checking the fields for the database. We can see what are the most common values based on each field. This allows us to give an idea of what we can filter and what we propose to do further EDA analysis and build upon with regression models and other techniques. This also shows the frequency in which numbers appear. Based on this, we�re able to make decisions to derive on further analysis
To emphasize this, most of the graphs that we see can be adjusted for modeling. Some variables such as employee full time and part time were excluded and the employee total was utilised to reduce features. Some variables were skewed, and required min-max transformations and/or removal of outliers to increase normality.
 
### 4.2.3 Pearson Correlation Matrix

Correlation matrix shows how well two numeric variables are associated with each other. Correlation coefficient measures the extent of the above mentioned relationship. 
The plot below shows Pearson's coefficient for the numeric variables in our dataset.
 
<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/others/pc.png" width="389" />

Highlighted values show moderate to strong correlation. Note that high correlation between two variables does not imply that one causes the other.
            dep_delay month day_of_week dep_time arr_delay air_time taxi_out taxi_in   age
dep_delay        1.00 -0.23       -0.21     0.17      0.90    -0.14     0.17   -0.11 -0.14
month           -0.23  1.00       -0.11    -0.16     -0.27    -0.14    -0.24   -0.13 -0.14
day_of_week     -0.21 -0.11        1.00    -0.14     -0.28    -0.11    -0.21   -0.13 -0.10
dep_time         0.17 -0.16       -0.14     1.00      0.04    -0.22    -0.13   -0.31 -0.07
arr_delay        0.90 -0.27       -0.28     0.04      1.00    -0.18     0.49    0.08 -0.20
air_time        -0.14 -0.14       -0.11    -0.22     -0.18     1.00     0.02    0.07 -0.45
taxi_out         0.17 -0.24       -0.21    -0.13      0.49     0.02     1.00   -0.06 -0.20
taxi_in         -0.11 -0.13       -0.13    -0.31      0.08     0.07    -0.06    1.00 -0.29
age             -0.14 -0.14       -0.10    -0.07     -0.20    -0.45    -0.20   -0.29  1.00

#### 4.2.3.1 Interpretation
The plot and table above shows a strong correlation between dep_delay and arr_delay (0.90). There is moderate correlation between arr_delay and taxi_out (0.49).
 
## Multicollinearity problem 

When there is multicollinearity present in our variables, it would impede our interpretation of the coefficients of the model due to the confounding variable. When fitting a multivariate linear regression model, the independent variables are called partial coefficients, however it might be representing the true effect of the independent variable. The association with other independent variables would create a proxy effect which makes the coefficient presented in the multivariate model misleading. To avoid having the multicollinearity problem, we conduct Pearson correlation, Chi-Square, and point-biserial correlation test to test the association among variables. With the initial results of these tests, it would be used to supplement our decision in removal of variables in model selection. To add on to it, Variable Inflation factor (VIF) would be done to test our regression model for 
multicollinearity among numerical variables. 

### Chi-square independence test 
Chi-square test is a statistical hypothesis test which is non-parametric, meaning that it does not assume any underlying distribution, for example, linearity (The Chi-Square Test of Independence, 2013). 
 
H0: Independent 
HA: Dependent 
0.05 is used as the critical value, if p-value < 0.05, we will reject the null hypothesis, thus the variables are dependent. 

To have a preliminary idea of whether categorical variables are associated with each other, we conducted a few iterations of the chi-square independence test of one categorical variable against the others. It is evident that all categorical variables are highly dependent on each other. 

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/others/chi.png" width="396" />
 
### Point-biserial correlation test 
Point biserial correlation test is used when one variable is numerical and another is dichotomous. One of the assumptions for this test is the normality of the numerical variable. In our case, none of our numerical variables are normal. The test was performed between our numerical and categorical variables and the calculated results were very close to zero.
 
# Modeling
 
## Min-Max Normalization & Dummy variables 
Min-max normalization transforms our numerical variables to a range between 0 to 1. Rescaling is essential to interpret the results of the regression models as all the numerical variables would have the same scale. 
When fitting in the regression models, R would automatically generate n-1 dummy variables according to n factors in a categorical variable. Since the categorical variables in our data are not ordinal, dummy variables are more appropriate than label encoding (Sethi, 2020).

## MV ln. model summary
Initially, a multivariate linear regression model was chosen to investigate the relationships between airline on-time performance and each of the independent variables. From the exploratory analysis, several states are determined to house the most flights, and therefore, the greatest frequency of delays. California contains multiple primary airline hubs for each of the three mainline carriers. With this knowledge, a subset of data containing information from just California was used to potentially generalise flight delays across the country.
The variables of the month, day of the week, destination state, departure time, airline, taxi in and out time, origin airport, destination airport, flight time, manufacturer, model, and age were initially modeled. By observing the statistical significance of the coefficients in several variables, some feature reduction was performed. In addition, the Boruta algorithm was run across variables to determine variable importance. 
<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/LM Plots/boruta_significance.png" width="461" />
One assumption we made was that the slope of the regression line fit for each category is equal as dummy variables could only impact the intercept of the linear regression model. Beyond looking at the result of the point-biserial correlation test conducted, we can fit a model that allows slope to differ. To capture the interaction between categorical and numerical variables, we included interaction variables on the variables that were determined to be the most important by the Boruta algorithm. The interaction variable terms were statistically insignificant, which coincided with the result of the point-biserial correlation test. Therefore, we won�t keep it as there is no significant difference between the slopes of different categories. 
Through several iterations, a multivariate linear regression containing month, departure time, airline, and age were determined to be the most impactful variables. An R-Squared value of 0.02108 and p-value of less than 2.2e^-16 were calculated. VIF and residual plots were generated based on the iterated model. VIF for the initial model cannot be generated because there are coefficients that are highly correlated to each other. In further iterations, numerical variables with a VIF larger than 5 were taken out. In the final model , all the VIF values are smaller than 5, meaning there is no collinearity. 
 ## Analysis of MLM
Analysis of the model requires interpretation of the calculated statistics run on the resulting model. VIF values suggest a lower correlation between variables, which satisfies the assumptions for a linear model. The low p-value of the coefficients suggest that the model has statistical significance. However, the low R-Squared value describes a model that does not well encapsulate a large proportion of the variance in the dataset.
The residual plots seen below elucidate a few findings regarding the dataset. In the Residual vs. Fitted plot, patterns are difficult to view as the number of individual flights is quite high, however, residuals do not appear to be spread equally. A larger portion of the dataset has values above the horizontal line.
<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/LM Plots/normal_qq.png" width="372" /><img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/LM Plots/residual_vfitted.png" width="372" /><img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/LM Plots/scale_location.png" width="372" /><img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/LM Plots/cooks_distance.png" width="372" />
In the normal Q-Q plot, the residuals do not follow a linear line above around 1 theoretical quantile. This suggests that the residuals are not normally distributed. The scale-location plot contains very distinct patterns which suggest abnormal behaviour of the residuals with this linear model. Lastly, the residuals spread in the residual vs leverage plot suggest that all cases are within Cook�s distance lines and no individual flights are particularly influential to the model.
This suggests that further transformation of the variables is necessary to better fit a linear model, or that a different type of model would perform better. However, it is important to note that the modeling showed that several variables are important and influence aircraft performance more than others. Of these, the US summer months between May and August, departure time later in the day, and older aircraft age contribute greatly to increasing aircraft departure delays.
## BINOMIAL ln model summary
Analysis of the residuals in the multivariate linear model shows that this model may not be the best method to model departure delays. A summary of on-time performance shows that the median of flights depart 3 mins earlier than anticipated, and the distribution of on-time performance skews to the left with a right-hand tail. A summary of on-time performance shows that on delays that are 1 minute or greater, the median delay is 12 minutes long with a mean of 20 minutes. Since costs increase as delays increase, transformations may be useful to model the flights with greater delays.
Therefore, on-time performance was then categorized into a binary category with flights without a meaningful delay (12 minutes or less) and flights with a longer delay (13 or more minutes). A binary, or logistic, regression model was then utilized to model the effect of variables and then compared to the earlier multivariate linear regression by observing the statistical significance of variables, and a simulated residual plot. The data were then randomly split into 75% testing and 25% training data for validation purposes. 
The model was then also subset specifically for American Airlines to determine the effect of departure time, month, and aircraft model type. The results are several significant variables that include specific months and specific model types. An AIC value of 363,681 was calculated after 4 Fisher Scoring iterations, nearly halved from the AIC value using the original 14 variables. 
Similarly, United and Delta airlines were modeled individually and AIC for each is calculated to be 125,161 and 226,094, respectively. With these models, comparisons between corresponding significant variables of each airline can explain strengths and weaknesses between American Airlines� major competitors. Delta has negative coefficients across the board for all models of aircraft, United has half positive and half negative, but American has positive coefficients for all models of aircraft except for the Airbus A320.
## Analysis
The relative reduction in AIC compared to the original model with most variables shows that the reduction to these three variables has improved the explanatory power of this model.
American Airlines contained 266,599 observations in its training set. 88,936 observations were then used to validate the model and the resulting confusion matrix is shown here. 
<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/LM Plots/binomial_residual_plot.png" width="355" />
In order to view the models� fit on residuals, a DHARMa function was used to create scaled residuals by simulating residuals from the models. In both the Q-Q plot and the residual vs. predicted plots, residuals appear to be handled well by the model.
For each airline, the months of April through August had a positive coefficient and significant p-values suggesting that these months will see higher delays across the board. In our EDA, we note that these months do not necessarily have a higher flight number than other months, and therefore may not be attributed to an increase in flights due to the summer. However, these months certainly do coincide with the typical season for extreme weather events such as tornadoes and hurricanes. In all cases, the time of day also contributed to a longer delay, but only marginally. 
However, utilizing the confusion matrix, we can calculate the overall accuracy of the model to be 54.2%, suggesting that further refinements can be made, or that more specific inferences surrounding the cause of delays are needed to better improve the model.

# Limitations
 
## Dataset limitations
The dataset we obtained was very rich, with around 12 million observations and approximately 65 variables, the size was around 8 GB. Challenges arise from dealing with a huge dataset such as ours, it gets complicated to run on R if we don�t subset the dataset. To overcome such challenges, the feather package from R was used to load and write data so we could read and write the data without our computer crashing.
When the Aircraft dataset was merged with our main dataset (BTS) using the aircraft tail number, 18% of the tail numbers were missing from the BTS data set and were excluded from the analysis.
At first, we tried to get Weather data using 2 different APIs, however, since our dataset contained millions of observations we had to find a different way to get this data since we had a limitation on the number of calls we could perform daily. API calls were also failing at times with �Access denied� errors for some airports. It could not be explained since it was working for other airports at the same time with the same API key.
In the end, we downloaded CSV files for weather stations located in or around the top 50 airports in terms of domestic flight volume. This information was not taken into consideration for this model and will be reserved for future modeling.
## Model limitations
In our analysis, more weight was put on correlation tests and EDA to verify the insights we obtained from regression as our confidence in the regression models are low.
One limitation that should be taken into account is that the response variable is positively skewed which violates the normality assumption. To overcome the skewness of the distribution, one could consider sqrt transformation to departure delay and perform data trimming on the tails to remove outliers. Nevertheless, even if the normality assumption was satisfied, the violation of the assumption that observations are independent of each other cannot be solved. 
Although bifurcation of the departure delay into a binomial variable helped in modeling through logistic regression, the model reduces the granularity and explainability of the data itself. Even with high accuracy, the model cannot discern the relationship between the variables and a delay of 15 minutes or a delay that may be 90 minutes long.
Our data is of time-series nature, as shown in EDA, if a flight is delayed at 8:30 am, for example, it will affect the departure time of ongoing flights at a later time delay as well. From the residual plots, the residuals aren�t independently normally distributed(i.i.d) and it shows there is autocorrelation between residuals. The limitation of linear and binomial regression models could be overcome by other appropriate time series analysis models such as Seasonal ARIMA. Even though our confidence in these regression models is very low, linear regression gives us a rough idea of the relationship between variables. 
For time series analysis which can be conducted in later stages, when modeling intervention models, a regression model is needed. For example, the time series before the interventions was modeled by the seasonal ARIMA (1,0,0) x (0,1,0)12, a regression model is needed to describe the relationship before and after the intervention. The existing regression models would be an asset/template for utilizing regression as a tool. 

 
## Conclusion
  
## References
 
Jim Frost,(n.d.). Multicollinearity in Regression Analysis: Problems, Detection,and Solutions. Statisctics By Jim. https://statisticsbyjim.com/regression/multicollinearity-in-regression-analysis/
Kim, N. Y., & Park, J. W. (2016). A study on the impact of airline service delays on emotional reactions and customer behavior. Journal of Air Transport Management, 57, 19�25. https://doi.org/10.1016/j.jairtraman.2016.07.005
American Airlines Reports First-Quarter 2021 Financial Results. American Airlines News Room, 2021. https://news.aa.com/news/news-details/2021/American-Airlines-Reports-First-Quarter-2021-Financial-Results-CORP-FI-04/default.aspx
Ghosh,I. (2020). This chart shows how airlines are being grounded by COVID-19. World Economic Forum. https://www.weforum.org/agenda/2020/03/this-chart-shows-how-airlines-are-being-grounded-by-covid-19/
Maynard,M. (2015). How To Survive July, The Busiest Air Travel Month Of The Year. Forbes.com. https://www.forbes.com/sites/michelinemaynard/2015/07/06/how-to-survive-the-busiest-air-travel-month-of-the-year/?sh=7f98a7c23506
Ball, M. (2010, November). Total Delay Impact Study A Comprehensive Assessment of the Costs and Impacts of Flight Delay in the United States. https://isr.umd.edu/NEXTOR/pubs/TDI_Report_Final_11_03_10.pdf
U.S. Passenger Carrier Delay Costs. Airlines for America, 2020. https://www.airlines.org/dataset/u-s-passenger-carrier-delay-costs/. 
The leading airlines worldwide in 2021, ranked by brand value. Statista 2021. https://www.statista.com/statistics/275944/brand-value-of-airlines/
Market value of selected airlines worldwide as of April 2021. Statista 2021. https://www.statista.com/statistics/275948/market-capitalization-of-selected-airlines/
Key figures of the four largest aircraft manufacturers worldwide in FY 2020. Statista 2020. https://www.statista.com/statistics/269920/key-figures-of-the-four-largest-aircraft-manufacturers/
Radka, R. (2021). Airline Hub Guide: Which U.S. Cities Are Major Hubs and Why it Matters. https://www.airfarewatchdog.com/blog/50066526/airline-hub-guide-which-u-s-cities-are-major-hubs-and-why-it-matters/
The Chi-square test of independence. (2013). PubMed Central (PMC). https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3900058/#:%7E:text=The%20Chi%2Dsquare%20test%20is,variables%20is%20nominal%20or%20ordinal.
University of Southampton. (n.d.). Chi Square. Is there a statistically significant relationship between a student�s Year 11 truancy and his or her enrolment in full time education after secondary school? https://www.southampton.ac.uk/passs/full_time_education/bivariate_analysis/chi_square.page
Statistics Solutions. (2021). ANOVA. https://www.statisticssolutions.com/free-resources/directory-of-statistical-analyses/anova/#:%7E:text=ANOVA%20assumes%20that%20the%20data,are%20independent%20of%20each%20other
Sethi, A. (2020). Categorical Encoding | One Hot Encoding vs Label Encoding. Analytics Vidhya. https://www.analyticsvidhya.com/blog/2020/03/one-hot-encoding-vs-label-encoding-using-scikit-learn/



## Appendix
 

```r
  library(psych)
  library(devtools)
  library(tidyverse)
  library(dplyr)
  library(ggplot2)
  library(Amelia)
  library(knitr)
```
 
 
To get the latest content, we are using a web API call for Airport Names. The `httr::get` will assist us in fetching the content in the JSON format. API key is being used for authenticating our call with the API provider. Since JSON cannot be directly consumed by regression packages, we deploy `jsonlite::fromJSON` to convert to an R dataframe.
 

```r
library(httr)
library(jsonlite)
library(dplyr)
icao <- GET(
  url = 'https://applications.icao.int/dataservices/api/safety-characteristics-list?api_key=8d00ef90-0982-11ec-9d72-8160549d64ab&airports=&states=USA'
)
response <- content(icao, 'parsed')
API_data <- fromJSON(response)
#Only pick those columns that are useful later on
API_data <- API_data %>% select(airportCode, airportName)
```
 
Scrapping AIrfleet data from web

```r
# Explicit URL
url <- 'https://www.planemapper.com/airlines/AAL'
AA <- url %>%
  read_html() %>%
  html_nodes(xpath='//*[@id="aircrafts"]') %>%
  html_table()
AA_fleet <- AA[[1]]
View(AA_fleet)
# Write AA_fleet to feather
write_feather(AA_fleet, here('AA_fleet.feather'))
# Explicit URL
swaurl <- 'https://www.planemapper.com/airlines/SWA'
SWA <- swaurl %>%
  read_html() %>%
  html_nodes(xpath='//*[@id="aircrafts"]') %>%
  html_table()
SWA_fleet <- SWA[[1]]
View(SWA_fleet)
# Write AA_fleet to feather
write_feather(SWA_fleet, here('SWA_fleet.feather'))
# Explicit URL
jbuurl <- 'https://www.planemapper.com/airlines/JBU'
JBU <- jbuurl %>%
  read_html() %>%
  html_nodes(xpath='//*[@id="aircrafts"]') %>%
  html_table()
JBU_fleet <- JBU[[1]]
# Write AA_fleet to feather
write_feather(JBU_fleet, here('JBU_fleet.feather'))
# Explicit URL
dalurl <- 'https://www.planemapper.com/airlines/DAL'
DAL <- dalurl %>%
  read_html() %>%
  html_nodes(xpath='//*[@id="aircrafts"]') %>%
  html_table()
DAL_fleet <- DAL[[1]]
# Write AA_fleet to feather
write_feather(DAL_fleet, here('DAL_fleet.feather'))
ualurl <- 'https://www.planemapper.com/airlines/UAL'
UAL <- ualurl %>%
  read_html() %>%
  html_nodes(xpath='//*[@id="aircrafts"]') %>%
  html_table()
UAL_fleet <- UAL[[1]]
# Write AA_fleet to feather
write_feather(UAL_fleet, here('UAL_fleet.feather'))
```
 
Merging Airfleet data into our dataset
 

```r
# Load Files ----
maindf <- read_feather(here('clean_3airlines.feather'))
delta <- read_feather(here('DAL_fleet.feather'))
american <- read_feather(here('AA_fleet.feather'))
united <- read_feather(here('UAL_fleet.feather'))
# Join Files ----
allrows <- bind_rows(delta, american, united)
testjoin <- left_join(maindf, allrows, by = c('tail_num' = 'Tail'))
col_status <- status(testjoin)
# Clean column names ----
clean_join <- clean_names(testjoin)
# Separate the age/year columns into two columns
separate <- clean_join %>%
  separate(age_built, c('age', 'year'))
status(separate)
```
 
Airline On-time data

```r
ontime_raw <- read.csv("https://raw.githubusercontent.com/charlottetse33/36103_Logistics-Transport-Aviation/main/test%20on%20time%20report.csv")
```
Airline DOT_ID corresponding to Airline Names

```r
#Seperate loading data to prevent R from crashing
id_airline <- read.csv("https://raw.githubusercontent.com/charlottetse33/36103_Logistics-Transport-Aviation/main/dot_id_airline.csv")
```
Merge Airline Names with On-time Dataset

```r
colnames(id_airline) <- c("DOT_ID_Reporting_Airline", "Airline")
 
ontime_1 <- left_join(ontime_raw, id_airline, by = "DOT_ID_Reporting_Airline")
```
Merge API Airport names with On-time Dataset

```r
ontime_2 <- ontime_1 %>% mutate(Origin_airportCode = paste("K",Origin, sep = ""), Dest_airportCode = paste("K",Dest, sep = ""))
Originjoint <- left_join(ontime_2, API_data, by = c("Origin_airportCode" = "airportCode"))
names(Originjoint)[names(Originjoint) == "airportName"] <- "Origin_airportName"
ontime_final <- left_join(Originjoint, API_data, by = c("Dest_airportCode" = "airportCode"))
names(ontime_final)[names(ontime_final) == "airportName"] <- "Dest_airportName"
#New column names from merging data:
#Airline, Origin_airportName, Dest_airportName
```
Adding fleet data into ontime dataset

```r
maindf <- read_feather(here('clean_3airlines.feather'))
delta <- read_feather(here('DAL_fleet.feather'))
american <- read_feather(here('AA_fleet.feather'))
united <- read_feather(here('UAL_fleet.feather'))
# Join Files ----
allrows <- bind_rows(delta, american, united)
testjoin <- left_join(maindf, allrows, by = c('tail_num' = 'Tail'))
col_status <- status(testjoin)
# Clean column names ----
clean_join <- clean_names(testjoin)
# Separate the age/year columns into two columns
separate <- clean_join %>%
  separate(age_built, c('age', 'model_year'))
status(separate)
# Save a feather file
write_feather(separate, here('clean_3airline_fleet.feather'))
```
Adding Latitude and Longitude information by state into dataset

```r
library(feather)
library(here)
library(tidyverse)
library(future)


feather_df <- read_feather("clean_3airline_fleet_employ.feather")
state_coord <- read.csv(file = "state_coord.csv")
air_coord <- read.csv(file = "air_coord.csv")
## Merge Origin latitude and Longitude by state
o_state_coord <- select(state_coord, ORIGIN_STATE_ABR, latitude, longitude)
d_state_coord <- select(state_coord, DEST_STATE_ABR, latitude, longitude)
leftJoin_origin <- left_join(x = feather_df, y = o_state_coord, by="ORIGIN_STATE_ABR")
names(leftJoin_origin)[names(leftJoin_origin) == "latitude"] <- "ORIGIN_STATE_LATITUDE"
names(leftJoin_origin)[names(leftJoin_origin) == "longitude"] <- "ORIGIN_STATE_LONGITUDE"
leftjoin_origin_1 <- leftJoin_origin %>% relocate(c("ORIGIN_STATE_LATITUDE","ORIGIN_STATE_LONGITUDE"), .after = "ORIGIN_STATE_ABR")
## Merge Destination latitude and Longitude by state
leftJoin_dest <- left_join(x = leftjoin_origin_1, y = d_state_coord, by="DEST_STATE_ABR")
names(leftJoin_dest)[names(leftJoin_dest) == "latitude"] <- "DEST_STATE_LATITUDE"
names(leftJoin_dest)[names(leftJoin_dest) == "longitude"] <- "DEST_STATE_LONGITUDE"
leftjoin_dest_1 <- leftJoin_dest %>% relocate(c("DEST_STATE_LATITUDE","DEST_STATE_LONGITUDE"), .after = "DEST_STATE_ABR")
## Write feather
write_feather(leftjoin_dest_1, "C:/Users/gerar/OneDrive/Escritorio/MDSI/STDS/AT2/EDA/EDA/clean.feather")
```

Adding Latitude and Longitude information by state into dataset

```r
library(feather)
library(here)
library(tidyverse)
library(future.apply)
feather2_df <- read_feather("clean.feather")
air_coord <- read.csv(file = "air_coord2.csv")
## Merge Origin latitude and Longitude by AIRPORT
o_air_coord <- select(air_coord, ORIGIN_AIRPORT_CODE, latitude, longitude)
d_air_coord <- select(air_coord, DEST_AIRPORT_CODE, latitude, longitude)
leftJoin_origin_air <- left_join(x = feather2_df, y = o_air_coord, by="ORIGIN_AIRPORT_CODE")
names(leftJoin_origin_air)[names(leftJoin_origin_air) == "latitude"] <- "ORIGIN_AIRPORT_LATITUDE"
names(leftJoin_origin_air)[names(leftJoin_origin_air) == "longitude"] <- "ORIGIN_AIRPORT_LONGITUDE"
leftjoin_origin_air_1 <- leftJoin_origin_air %>% relocate(c("ORIGIN_AIRPORT_LATITUDE","ORIGIN_AIRPORT_LONGITUDE"), .after = "ORIGIN_AIRPORT_CODE")
## Merge Destination latitude and Longitude by AIRPORT
leftJoin_dest_air <- left_join(x = leftjoin_origin_air_1, y = d_air_coord, by="DEST_AIRPORT_CODE")
names(leftJoin_dest_air)[names(leftJoin_dest_air) == "latitude"] <- "DEST_AIRPORT_LATITUDE"
names(leftJoin_dest_air)[names(leftJoin_dest_air) == "longitude"] <- "DEST_AIRPORT_LONGITUDE"
leftjoin_dest_air_1 <- leftJoin_dest_air %>% relocate(c("DEST_AIRPORT_LATITUDE","DEST_AIRPORT_LONGITUDE"), .after = "DEST_AIRPORT_CODE")
write_feather(leftjoin_dest_air_1, "C:/Users/gerar/OneDrive/Escritorio/MDSI/STDS/AT2/EDA/EDA/clean_3airline_fleet_employ_coord.feather")
```
Adding employee data into ontime dataset

```r
allmonths <- read_feather("C:/Users/tsetc/Downloads/clean_3airline_fleet (1).feather")
#This dataset includes airline, origin_airportname, dest_airportname
names(allmonths) <- toupper(names(allmonths))
# read employee dataset
employee_data <- read_csv("https://raw.githubusercontent.com/timothywallaby/36103_Logistics-Transport-Aviation/main/Employment%20dataset%202019-2021.csv")
# concentenate variables for employee dataset
employee_data$combine <- paste(employee_data$YEAR, employee_data$MONTH, employee_data$CARRIER_NAME, sep = "_")
employee_data <- employee_data %>% select(combine, EMPFULL, EMPPART, EMPTOTAL, EMPFTE)
# concentenate variables for big dataset
allmonths$combine <- paste(allmonths$YEAR, allmonths$MONTH, allmonths$AIRLINE, sep = "_")
# Combine 2 dataset
allmonths <- left_join(allmonths, employee_data, by = 'combine')
allmonths <- allmonths %>% select(-combine)
write_feather(allmonths, "C:/Users/tsetc/Downloads/clean_3airline_fleet_employ.feather")
```

Plotting 

```r
library(tidyverse)
library(DataExplorer)
library(here)
library(funModeling)
library(Hmisc)
library(janitor)
library(feather)
library(future.apply)
library(data.table)

# Load data ----
allmonths <- read_feather(here('mlm_dataset_3.feather'))

# Overall status
status(allmonths)
summary_all <-  summary(allmonths)
summary_all <- as.data.frame(summary_all)
write_csv(summary_all, here('column_summary_statistics.csv'))

# Categorical overall
freq(allmonths, path_out = here('Column EDA 2', '.'))
freq(allmonths)
# Numerical Overall
plot_num(allmonths, path_out = here('Column EDA 2', '.'))
plot_num(allmonths)

# Not for EDA ---------------------------------------------------------------
Q1 <- quantile(allmonths$DEP_DELAY, .25)
Q3 <- quantile(allmonths$DEP_DELAY, .75)
IQR <- IQR(allmonths$DEP_DELAY)

allmonths2 <- subset(allmonths, allmonths$DEP_DELAY > (Q1 - 1.5*IQR) & 
                       allmonths$DEP_DELAY< (Q3 + 1.5*IQR))

Q1 <- quantile(allmonths$ARR_DELAY, .25)
Q3 <- quantile(allmonths$ARR_DELAY, .75)
IQR <- IQR(allmonths$ARR_DELAY)

allmonths2 <- subset(allmonths2, allmonths2$ARR_DELAY > (Q1 - 1.5*IQR) & 
                       allmonths2$ARR_DELAY< (Q3 + 1.5*IQR))

Q1 <- quantile(allmonths$ARR_DELAY_NEW, .25)
Q3 <- quantile(allmonths$ARR_DELAY_NEW, .75)
IQR <- IQR(allmonths$ARR_DELAY_NEW)

allmonths2 <- subset(allmonths2, allmonths2$ARR_DELAY_NEW > (Q1 - 1.5*IQR) & 
                       allmonths2$ARR_DELAY_NEW< (Q3 + 1.5*IQR))

plot_num(allmonths2)


num_col <- select_if(allmonths, is.numeric)

num_col <- num_col %>% drop_na()

#i in seq_along(num_col)

num_col <- num_col %>% 
  select('dep_delay', 'dep_delay_new', 'taxi_out', 'taxi_in',
         'arr_delay', 'arr_delay_new', 'air_time', 'distance',
         'age', 'carrier_delay', 'weather_delay', 'nas_delay',
         'security_delay', 'late_aircraft_delay', 'total_add_gtime',
         'empfull', 'emppart', 'emptotal', 'empfte')

for (i in 1:9) {
  if (max(num_col[,i]) > (mean(unlist(num_col[,i])) + 4* sd(unlist(num_col[,i])))) {
    num_col <- num_col %>% arrange(num_col[,i])
    num_col <- num_col[round(nrow(num_col) *0.01, digits = 0):round(nrow(num_col)* (1-0.01) , digits = 0),]
  }
}

#Min-max transformation 
min_max_norm <- function(x){
  (x-min(x)) / (max(x) - min(x))
}
num_col_norm <- as.data.frame(future_lapply(num_col, min_max_norm))

plot_num(num_col_norm)

status(num_col_norm)
status(num_col)
status(allmonths)

# Individual Column Assessment ---------------------------------------------
names(allmonths)

# Determine Outlier range for *delays only 1 min and greater*
onlydelay <- allmonths %>% 
  filter(dep_delay > 0)
Q3 <- quantile(onlydelay$dep_delay_new, .75)
IQR <- IQR(onlydelay$dep_delay_new)
Outlier <- Q3 + 1.5*IQR
Outlier
Q3

# Must use a package to make plotting faster
# filter out outliers of delays
allmonth_plot <- na.omit(allmonths)
allmonth_plot <- allmonth_plot %>% 
  filter(dep_delay <= 95)

allmonth_plot %>% 
  sample_n(50000) %>% 
  ggplot(aes(x=dep_delay, y=year)) +
  geom_point(alpha=0.3)

allmonth_plot %>% 
  sample_n(50000) %>% 
  ggplot(aes(x=dep_delay, y=month)) +
  geom_boxplot(alpha=0.2) +
  geom_point(alpha=0.3)

allmonth_plot %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=dep_delay, x=air_time)) +
  geom_hex() +       
  scale_fill_viridis_c() +
  geom_point(shape = '.', col = 'white')

allmonth_plot %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=dep_delay, x=distance)) +
  geom_hex() +       
  scale_fill_viridis_c() +
  geom_point(shape = '.', col = 'white')
# Check correlation to Air Time

cor(allmonth_plot$air_time, allmonth_plot$distance) #0.9742272 correlation

allmonth_plot %>% 
  filter(air_time > 0) %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=air_time, x=distance)) +
  geom_point(alpha = 0.3)


allmonth_plot %>% 
  filter(dep_delay > 0) %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=dep_delay, x=age)) +
  geom_hex() +       
  scale_fill_viridis_c() +
  geom_point(shape = '.', col = 'white')

allmonth_plot %>% 
  filter(dep_delay < 0) %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=dep_delay, x=age)) +
  geom_hex() +       
  scale_fill_viridis_c() +
  geom_point(shape = '.', col = 'white')

summary(allmonth_plot$age)
# median is 20 years of age anyway, no wonder we see most observations there.

allmonths %>% 
  filter(dep_delay > 95) %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=dep_delay, x=age)) +
  geom_hex() +       
  scale_fill_viridis_c() +
  geom_point(shape = '.', col = 'white')
#even among outliers, not much else to say

allmonth_plot %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=dep_delay, x=taxi_out)) +
  geom_hex() +       
  scale_fill_viridis_c() +
  geom_point(shape = '.', col = 'white')

allmonth_plot %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=dep_delay, x=taxi_in)) +
  geom_hex() +       
  scale_fill_viridis_c() +
  geom_point(shape = '.', col = 'white')
 #doesn't seem as though taxi in and out have much effect on delays
  #perhaps longer taxi is because they were early?

allmonth_plot %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=dep_delay, x=carrier_delay)) +
  geom_hex() +       
  scale_fill_viridis_c() +
  geom_point(shape = '.', col = 'white')

allmonth_plot %>% 
  sample_n(50000) %>%
  filter(dep_delay > 0) %>% 
  filter(dep_delay < 500) %>% 
  ggplot(aes(y=dep_delay, x=dep_time)) +
  scale_fill_viridis_c() +
  geom_point(alpha = 0.3)
  #view when start of day is
  #delays tend to increase later in the day

allmonth_plot %>% 
  sample_n(50000) %>% 
  filter(dep_delay > 0) %>% 
  ggplot(aes(y=dep_delay, x=manufacturer)) +
  scale_fill_viridis_c() +
  geom_point(alpha = 0.3)

allmonth_plot %>% 
  sample_n(50000) %>% 
  #filter(dep_delay > 0) %>% 
  ggplot(aes(y=dep_delay, x=model)) +
  scale_fill_viridis_c() +
  geom_point(alpha = 0.3)
# manufacturer and model type need to be cleaned
```

More EDA

```r
library(tidyverse)
library(here)

library(httr)
library(jsonlite)
library(dplyr)
library(magrittr)
library(feather)


# Load data ----

delays <- read_feather(here("mlm_dataset_4time.feather"))

delays_reduced <- delays %>% sample_n(500000)

# View columns

names(delays)

# Plot histogram of delays

delays %>% 
  filter(dep_delay < 300) %>% 
  ggplot(aes(x=dep_delay)) +
  geom_histogram()

# Plot some relationships

delays %>% # delay as a function of flight time
  #filter(arr_delay > 0) %>% 
  #filter(arr_delay < 60) %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=arr_delay, x=air_time, col = airline)) +
  geom_point(alpha=0.1, show.legend = F) +
  #geom_smooth(method='lm', show.legend = F) +
  facet_wrap(~airline) +
  scale_color_viridis_d() +
  theme_minimal() +
  ylim(0, 150) +
  labs(title = 'Arrival Delay by Flight Time',
       x = 'Flight Time (mins)',
       y = 'Arrival Delay (mins)')

slm <- lm(arr_delay ~ taxi_out, data = delays)
coef(slm)
summary(slm)

plot(slm)

delays %>% # delay as a function of taxi_out
  #filter(arr_delay > 0) %>% 
  #filter(arr_delay < 60) %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=arr_delay, x=taxi_out, col = airline)) +
  geom_point(alpha=0.1, show.legend = F) +
  geom_smooth(method='lm', show.legend = F) +
  facet_wrap(~airline) +
  scale_color_viridis_d() +
  theme_minimal() +
  ylim(0, 150) +
  labs(title = 'Arrival Delay by Taxi Out Time',
       x = 'Taxi Out (mins)',
       y = 'Arrival Delay (mins)')


delays %>% # delay as a function of taxi_in
  #filter(arr_delay > 0) %>% 
  #filter(arr_delay < 60) %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=arr_delay, x=taxi_in, col = airline)) +
  geom_point(alpha=0.1, show.legend = F) +
  #geom_smooth(method='lm', show.legend = F) +
  facet_wrap(~airline) +
  scale_color_viridis_d() +
  theme_minimal() +
  ylim(0, 150) +
  labs(title = 'Arrival Delay by Taxi In Time',
       x = 'Taxi In (mins)',
       y = 'Arrival Delay (mins)')

# Plot some Categorical Relationships:

delays %>% 
  filter(dep_delay > 0) %>% 
  ggplot() +
  geom_violin(aes(x=manufacturer, y=dep_delay, col = airline)) +
  facet_wrap(~airline) +
  scale_color_viridis_d() +
  theme_minimal()

delays %>% 
  ggplot() +
  geom_bar(aes(x = manufacturer, fill = airline)) +
  theme_minimal() +
  scale_color_viridis_d() +
  scale_fill_viridis_d() +
  theme_minimal() + 
  labs(title = 'Aircraft Manufacturer Count',
       x = 'Manufacturer',
       y = 'Number of flights')

delays %>% 
  ggplot() +
  geom_bar(aes(x = model, fill = airline)) +
  scale_color_viridis_d() +
  scale_fill_viridis_d() +
  theme_minimal() + 
  labs(title = 'Aircraft Model Count',
       x = 'Model',
       y = 'Number of flights')

  #remove embraer and mcdonnell as they represent very low values;
  #mcdonnell no longer in service

delays %>% 
  filter(manufacturer %in% c('boeing', 'airbus')) %>% 
  count(age, model) %>% 
  ggplot(aes(x = age, y = model)) +
  geom_tile(aes(fill = n))
  # 2 groups of ages appear. 
  # A320 proedominantly older craft
  # A321 predominatly younger craft
  # feature engineer buckets < 15, > 15
  
delays %>% # delay as a function of age
  filter(manufacturer %in% c('boeing', 'airbus')) %>%
  filter(model != '717') %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=arr_delay, x=age, col = airline)) +
  geom_point(alpha=0.1, show.legend = F) +
  geom_smooth(method='lm', show.legend = F) +
  facet_wrap(~airline) +
  scale_color_viridis_d() +
  theme_minimal() +
  ylim(0, 150) +
  labs(title = 'Arrival Delay by Aircraft Age',
       x = 'Age (years)',
       y = 'Arrival Delay (mins)')

delays %>% # delay as a function of age
  filter(manufacturer %in% c('boeing', 'airbus')) %>%
  filter(model != '717') %>% 
  sample_n(50000) %>% 
  ggplot(aes(y=air_time, x=age, col = airline)) +
  geom_point(alpha=0.1, show.legend = F) +
  #geom_smooth(method='lm', show.legend = F) +
  facet_wrap(~airline) +
  scale_color_viridis_d() +
  theme_minimal() +
  ylim(0, 150) +
  labs(title = 'Flight time by Aircraft Age',
       x = 'Aircraft Age (years)',
       y = 'Flight Time (mins)')


delays %>% 
  filter(manufacturer %in% c('boeing', 'airbus')) %>% 
  filter(dep_delay > 0) %>% 
  filter(year %in% c('2019')) %>% 
  count(month, dep_delay) %>% 
  ggplot(aes(x = month, y = dep_delay)) +
  geom_tile(aes(fill = n)) +
  labs(title = 'Flight Delays by Month',
       x = 'Month',
       y = 'Departure Delay (mins)')

library(funModeling)
library(Hmisc)
library(DataExplorer)

freq(delays %>% filter(year == '2019'))
freq(delays %>% filter(year == '2020'))

delays %>% 
  filter(manufacturer %in% c('boeing', 'airbus')) %>% 
  filter(dep_delay > 0) %>% 
  filter(dest_state_abr == 'CA') %>% 
  #filter(year %in% c('2019')) %>% 
  #sample_n(50000) %>% 
  #count(month, dep_delay) %>% 
  ggplot(aes(x = dep_time, y = dep_delay)) +
  geom_hex() +
  #scale_fill_viridis_d() +
  #geom_point(shape = 'o', col = 'blue', alpha = 0.1) +
  facet_wrap(~airline) +
  theme_minimal() +
  labs(title = 'Flight Delays by Time of Day in California',
       x = 'Time',
       y = 'Departure Delay (mins)')

delays %>% 
  filter(manufacturer %in% c('boeing', 'airbus')) %>% 
  filter(dep_delay > 0) %>% 
  filter(dest_state_abr == 'TX') %>% 
  #filter(year %in% c('2019')) %>% 
  #sample_n(50000) %>% 
  #count(month, dep_delay) %>% 
  ggplot(aes(x = dep_time, y = dep_delay)) +
  geom_hex() +
  #scale_fill_viridis_d() +
  #geom_point(shape = 'o', col = 'blue', alpha = 0.1) +
  facet_wrap(~airline) +
  theme_minimal() +
  labs(title = 'Flight Delays by Time of Day in Texas',
       x = 'Time',
       y = 'Departure Delay (mins)')


delays %>% 
  filter(manufacturer %in% c('boeing', 'airbus')) %>% 
  filter(dep_delay > 0) %>% 
  filter(dest_state_abr == 'TX') %>% 
  #filter(year %in% c('2019')) %>% 
  #sample_n(50000) %>% 
  #count(month, dep_delay) %>% 
  ggplot(aes(x = dep_time, y = dep_delay)) +
  geom_hex() +
  #scale_fill_viridis_d() +
  #geom_point(shape = 'o', col = 'blue', alpha = 0.1) +
  facet_wrap(~airline) +
  theme_minimal() +
  labs(title = 'Flight Delays by Time of Day in Illinois',
       x = 'Time',
       y = 'Departure Delay (mins)')



#delays %>% # plot count of distances, histogram?
  #filter(ARR_DELAY < 300) %>% 
  #ggplot(aes(x="air_time")) +
      #need to change distance to continuous variable
  #geom_bar()

#delays %>% # histogram of elapsed flight times
 # filter(arr_delay < 300) %>% 
  #ggplot(aes(x=ACTUAL_ELAPSED_TIME)) +
  #geom_histogram()

#delays %>% # delay as a function of flight time
  #filter(ARR_DELAY < 300) %>% 
  #ggplot(aes(y=ARR_DELAY, x=ACTUAL_ELAPSED_TIME)) +
  #geom_point() 

#delays %>% # may have collinearity
  #filter(ARR_DELAY < 300) %>% 
  #ggplot(aes(y=ACTUAL_ELAPSED_TIME, x=DISTANCE)) +
  #geom_point() 
    #appears to have pretty strong collinearity?
```

Correlation test + plot 

```r
 library(tidyverse)
library(here)
library(readr)
library(future.apply)
library(dplyr)
library(httr)
library(jsonlite)
library(RColorBrewer)
library(scales)
library(feather)
library(caret)
library(corrplot)
library(PerformanceAnalytics)
library(Hmisc)
# ========================
# Correlation test 
mlm_corr <- read_feather(here('Dataset', 'USE MLM 5 mlm_dataset_3.feather' ))
# get a random sample of 50,000 observations
 mlm_corr_n <- mlm_corr %>% sample_n(50000)
mlm_corr_n <- mlm_corr_n %>% select(dep_delay,month,day_of_week, dep_time, arr_delay, air_time, air_time,taxi_out,taxi_in,age)
corr_matrix <- cor(mlm_corr_n, method = "pearson", use = "complete.obs")
corr_matrix <-round(corr_matrix,3)
corr_matrix
corrplot(corr_matrix, method = "ellipse")
corrplot(corr_matrix, method = "pie")
corr_matrix_r <- rcorr(corr_matrix, type = c("pearson","spearman"))
corrplot(corr_matrix_r$r, type = "upper", order = "hclust",  
p.mat = corr_matrix_r$P, sig.level = 0.01, insig = "blank")
chart.Correlation(corr_matrix, histogram = TRUE, pch = 19)
# =========================
```

Clean data

```r
# Removing unused columns

clean_months <- clean_months %>% 
  select('year', 'quarter', 'month', 'day_of_month', 'day_of_week',
         'fl_date', 'tail_num', 'op_carrier_fl_num', 'origin_state_abr',
         'dest_state_abr', 'dep_time', 'dep_delay',
         'dep_delay_new', 'taxi_out', 'taxi_in', 'arr_time', 'arr_delay',
         'arr_delay_new', 'air_time', 'distance', 'carrier_delay',
         'weather_delay', 'nas_delay', 'security_delay',
         'late_aircraft_delay', 'first_dep_time', 'total_add_gtime',
         'airline', 'origin_airportname', 'origin_airport_code',
         'dest_airportname','dest_airport_code')

# Change column types

wrong_columns <- c('quarter', 'month', 'day_of_month', 'day_of_week',
                   'op_carrier_fl_num', 'dep_time', 'arr_time', 'first_dep_time')

clean_months[wrong_columns] <- future_lapply(clean_months[wrong_columns], factor)


# Check columns

col_status_cleaner <- status(clean_months)

#write interim feather file

write_feather(clean_months, here('clean_allairlines.feather'))

# Select only AA, DL, and UA
target = ('American Airlines inc.')

test <- clean_months %>% 
  filter(airline %in% c('American Airlines Inc.',
                        'Delta Air Lines Inc.',
                        'United Air Lines Inc.'))

unique(test$airline)

# Save new dataset

write_feather(test, here('clean_3airlines.feather'))

wrong_columns <- c('age', 'model_year')

clean_months['age'] <- future_lapply(clean_months['age'], as.numeric)
clean_months['model_year'] <- future_lapply(clean_months['model_year'], as.factor)


# Check columns

col_status_cleaner <- status(clean_months)

#write interim feather file

write_feather(clean_months, here('clean_3airline_fleet_employ_2.feather'))
```

Chi-square independence test + point-biseral test

```r
#chi-square independence test, dep_delay against other variables 
library(broom)
CHIS <- lapply(allmonths[,-1], function(x) chisq.test(allmonths[,1], x))
chi_result <- do.call(rbind, lapply(CHIS,tidy))

dmy <- dummyVars(" ~ . ", data= clean_months, fullRank = T)
dat_transformed <- data.frame(predict(dmy, newdata = clean_months))

#correlation test (including everything)
corr_result_all <- round(cor(dat_transformed), digits = 2)

sink('corr_result_all.txt')
corr_result_all
sink()
```


Linear regression code

```r
library(tidyverse)
library(here)
library(readr)
library(future.apply)
library(dplyr)
library(httr)
library(jsonlite)
library(RColorBrewer)
library(scales)
library(feather)
library(caret)
library(corrplot)
library(Boruta)


mlm_final <- read_feather(here('mlm_dataset_5.feather'))

# sqrt transoformation 
#mlm_final$dep_delay <- sqrt(mlm_final$dep_delay)


# Select California only as Subset

mlm_CA <- mlm_final %>% filter(origin_state_abr == 'CA')
names(mlm_CA)

mlm_all <- mlm_CA %>% 
  select(-origin_state_abr) %>% 
  droplevels()

str((mlm_all))

View(mlm)


# Numerical data transformation 
data <- mlm_all #change this to your data name 
trimming <- FALSE #change this to true if you want to trim data 



min_max_norm <- function(x){
  (x-min(x)) / (max(x) - min(x))
}

num_col <- select_if(mlm_all, is.numeric)

num_col_norm <- as.data.frame(lapply(num_col, min_max_norm))
cat_col <- mlm_all %>% select_if(negate(is.numeric))
num_col_norm$id <- seq.int(nrow(mlm_all))
cat_col$id <- seq.int(nrow(mlm_all))
combine_data <- left_join(num_col_norm, cat_col, by = 'id')
mlm_all <- combine_data %>% select(-id)

names(mlm_CA)
names(mlm_all)

# MLM on Most logical variables

mlm1 <- lm(dep_delay ~ month + day_of_week + dest_state_abr + dep_time +
             airline + taxi_out + origin_airport_code + dest_airport_code +
             air_time + taxi_in + manufacturer + model + age +
             emptotal, data = mlm_all)
summary(mlm1) # R-Squared 0.03944 p < 2.2e-16
plot(mlm1)

# MLM removal

mlm2 <- lm(dep_delay ~ month + day_of_week + dep_time +
             airline + taxi_out + origin_airport_code + dest_airport_code +
             air_time + model + age, data = mlm_all)
summary(mlm2) # R Squared 0.03184
plot(mlm2)


# MLM removal 2

mlm3 <- lm(dep_delay ~ month + day_of_week + dep_time +
             airline + taxi_out + origin_airport_code + 
            model + age, data = mlm_all)
summary(mlm3) # R-Squared 0.02715

# Run Boruta
boruta_sasuke <- Boruta(dep_delay ~ month + day_of_week + dep_time +
                        airline + taxi_out + origin_airport_code + 
                        model + age, data = mlm_all, doTrace = 2)

boruta_signif <- names(boruta_sasuke$finalDecision[boruta_sasuke$finalDecision %in% c("Confirmed", "Tentative")])
print(boruta_signif)
plot(boruta_sasuke, cex.axis = .7,
     las = 2, xlab ="", main = "Variable Importance")


# MLM boruta removal

mlm4 <- lm(dep_delay ~ month + dep_time +
             airline + taxi_out + origin_airport_code + 
             model + age, data = mlm_all)
summary(mlm4) # R-Squared  .02705


mlm5 <- lm(dep_delay ~ month + dep_time +
             airline + age, data = mlm_all)
summary(mlm5) # R-Squared .01202 p-value <2.2e-16



mlm6 <- lm(arr_delay ~ month + day_of_week + dep_time +
             airline + taxi_out + dest_airport_code +
             air_time + taxi_in + manufacturer + age,
             data = mlm_all)

summary(mlm6)

#improve upon mlm6 but added interaction varaible 
mlm_7 <- lm(dep_delay ~ month + dep_time +
              airline + age + month:age + 
              airline:age + airline:dep_time
            , data = mlm_all)

summary(mlm_7)
#interaction variable not significant --> no need to add interaction variable

#sqrt transformation 
mlm_final$dep_delay <- sqrt(mlm_final$dep_delay)

#VIF 
VIF(mlm5)
A1/VIF(mlm5)

summary_test

summary_txt <- summary(mlm1)

sink('second_summary.txt')
summary_txt
sink()

# Model diagnoistic 

pairs(mlm_CA)
corrplot(cor(mlm_CA_sub3), method = "number")



# Residual Plot on MLM 5

plot(mlm5)
```


```r
library(tidyverse)
library(here)
library(readr)
library(future.apply)
library(dplyr)
library(httr)
library(jsonlite)
library(RColorBrewer)
library(scales)
library(feather)
library(caret)
library(corrplot)
library(Boruta)
library(regclass)


# 1. Load Data -----
mlm_final <- read_feather(here('mlm_dataset_5.feather'))

summary(mlm_final)
#dep delay median is -3
#select delays greater than 0

blm_bino <- mlm_final %>% 
  filter(dep_delay > 0)

summary(blm_bino)
#dep delay median is 12, mean 20.8. 1Q 4, 3Q 30


# 2. Create new binomial delay

blm_bino <- blm_bino %>% 
  mutate(delay_new = dep_delay > 12)

summary(blm_bino)
#344677 true, #356513 false


# 3. Train/Test set data

blm_bino$id <- 1:nrow(blm_bino)
blm_bino.train <- blm_bino %>% dplyr::sample_frac(0.75)
blm_bino.test <- dplyr::anti_join(blm_bino, blm_bino.train, by ='id')


# 3. GLM model
glm0 <- glm(delay_new ~ month + day_of_week + dest_state_abr + dep_time +
              airline + taxi_out + origin_airport_code + dest_airport_code +
              air_time + taxi_in + manufacturer + model + age +
              emptotal, family = binomial(logit), data = mlm_bino.train)
summary(glm0)

glm1 <- glm(delay_new ~ month + dep_time +
              airline + taxi_out + 
              model + age, family = binomial(logit), data = mlm_bino.train)
summary(glm1)


# 4. Model only for AA

blm_aa.train <- blm_bino.train %>% 
  filter(airline == 'American Airlines Inc.')

blm_aa.test <- blm_bino.test %>% 
  filter(airline == 'American Airlines Inc.')

# 5. GLM model for AA

blm2 <- glm(delay_new ~ month + dep_time +
              model, 
              family = binomial(logit), data = blm_aa.train)
summary(blm2)


# 6. Model only for DL

blm_dl.train <- blm_bino.train %>% 
  filter(airline == 'Delta Air Lines Inc.')

blm_dl.test <- blm_bino.test %>% 
  filter(airline == 'Delta Air Line Inc.')

blm_ua.train <- blm_bino.train %>% 
  filter(airline == 'United Air Lines Inc.')

blm_ua.test <- blm_bino.test %>% 
  filter(airline == 'United Air Line Inc.')


# 7. GLM model for DL

blm3 <- glm(delay_new ~ month + dep_time +
              + model, 
            family = binomial(logit), data = blm_dl.train)
summary(blm3)

blm4 <- glm(delay_new ~ month + dep_time +
              model, 
            family = binomial(logit), data = blm_ua.train)
summary(blm4)

# 8. Look at VIF for models
VIF(glm1)
VIF(blm2)
VIF(blm3)
VIF(blm4)

1/VIF(blm2)
# 9 model validation

probability_aa <- predict(blm2, newdata = blm_aa.test, type='response')
prediction_aa <- ifelse(probability_aa > 0.5, 1, 0)
confusion_aa <- table(blm_aa.test$delay_new, prediction_aa)

confusion_aa


# 10. Plots
library(DHARMa)

res <- simulateResiduals(blm2, plot = T)

# Table

library(knitr)
kable(confusion_aa, caption = "Confusion Matrix")
```




Clean data
 
 
 
One or more appendices are the place to out details and ancillary materials.
These might include such items as
� Technical descriptions of (unusual) statistical procedures
� Detailed tables or computer output
� Figures that were not central to the arguments presented in the body of the report
� Computer code used to obtain results.
In all cases, and especially in the case of computer code, it is a good idea to add some text sentences
as comments or annotations, to make it easier for the uninitiated reader to follow what you are doing.
It is often difficult to find the right balance between what to put in the appendix and what to put in
the body of the paper. Generally you should put just enough in the body to make the point, and refer
the reader to specific sections or page numbers in the appendix for additional graphs, tables and other
details.

Final Dataset:
After joining all our datasets into one, we explored our data in detail:
Airlines were reduced to include only American Airlines and two main competitors (Delta and United Airlines), reducing observations from 12M to approximately 4M.
Observations missing the type of aircraft were removed, taking our observations down to 2.8M.
Column names were cleaned under the same format.
Variable selection, only variables that could represent a potential impact for airline delays were taken into consideration. Redundant (ie: 5 different fields indicating state: State, State ID,  State FIPS and State NM) and non important variables were removed, taking our total number of fields from 65 to 32 and finally to just 19.
Cleaning categorical variables that were incorrectly set as numerical.
In order to reduce the size of our data set and make it easier for all of us to handle it we used [data.table] and [feather] packages, taking it down from 7GB to 1.5 GB.
After doing this we continued with our variable inspections and removed the taxi-in and airtime variables with values below 0, which would indicate the flight did not happen.
Cleaning the Manufacturer observations, for example, grouping all the BOEING Values into one, BOEING, Boeing Charleston, Boeing SC, etc were transformed into just �Boeing�.
Cleaning the aircraft type variations by grouping all the similar types together, for example all the 737 similar variants such as 737 classic, next generation, 700, 800 and 900 were all classified as �737�.
Cleaning the Dep_Time variable by transforming it to a time variable (HH:MM) 24 hour time format using [hms], [as.POSIXct].


<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/EDA Plots/arrival_delay_by_taxi_in.png" width="542" />
When analyzing arrival delays and taxi in time we did not find a clear relation between these two variables, something interesting that we found here is that taxi in time is usually pretty low and therefore wont represent that big of an impact in the overall performance. It is important to note that American Airlines seems to not only have a higher average taxi-in time but also a bigger number of outliers in this regard.

<img src="C:/Users/goldt/Dropbox/School/UTS Sem 2 2021/36103 Statistical Thinking for Data Science/Assignment/Assignment 2/36103_Logistics-Transport-Aviation/EDA Plots/arrival_delay_by_taxi_out.png" width="542" />
Looking at taxi out time we found a higher relationship with arrival delays than with taxi-in. We also noticed that the taxi out times are considerably higher and therefore represent a bigger impact on the overall on-time performance.

### Summary Statistics
 

