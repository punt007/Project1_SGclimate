# Project 1: 
Exploring Climate Data of Singapore
Ponparis Gurdsapsri

## Introduction

This is Project 1 of the General Assembly Data Science Immersive course. The objective of this project is to explore the climate data of Singapore and to identify trends and patterns that can be used to make recommendations to the relevant stakeholders. The data used in the project can be obtained from [data.gov.sg](https://data.gov.sg/search). The data used in this project with data dictionary are as follow:

### Datasets
The datasets used in this project are number of raining day in a month and total volume of rainfall in a month and 5 other dataset relevant to weather, which are: relative humidity, maximum rainfall in a day, Average air temperature, hourly wet bulb temperature, and Average sunshine hour in a day. In additional to probelm statement, I also obtain data of visitor arrival in Singapore and used in this project as well. The additioanl data source is in below section.


#### Additional Data

Visitor arrival. Source from Singapore Tourism Board. Retrieved from https://www.singstat.gov.sg/publications/reference/ebook/industry/tourism

#### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|month|datetime|All dataset|Month of the year|
|total_rainfall|float|rainfall-monthly-total|Total rainfall in mm| 
|maximun_rainfall|float|rainfall-monthly-maximum-daily-total|Maximum rainfall in mm in a day|
|mean_sunshine|float|sunshine-duration-monthly-mean-daily-duration|Mean sunshine duration in hours|
|temp_mean_daily_min|float|surface-air-temperature-mean-daily-minimum|Mean daily minimum temperature in degree Celsius|
|no_of_rain_days|int|rainfall-monthly-number-of-rain-days|Number of days with rainfall more than 0.2mm|
|mean_rh|float|relative-humidity-monthly-mean|Mean relative humidity in percentage|
|total_visitors|int|Number of International Visitor Arrival|Total number of international visitor arrival in Singapore|

--


## Problem Statement

Background:
As ATC (Association of Trade & Commerce) Singapore. It is essense to help not just corporation and SMEs, but the individual business owner as well. One of the familiar business owner that can be found along the great Orchard Road and other tourism attraction places are the traditional ice-cream stand. They have been in business around haft a century, but now they're not doing so well now. Many of the owner are elder, hence ATC should help them to improve their business or at least help them to be more efficienct, help them take advantage from weather. The hottest period in the day would ideally be when people may want ice-cream the most, so setting up the stand at the right time and right place would be the key to success.

Objective:
The objective of this project is to develop the forecast of the hottest period in the day, so the ice-cream stand can be set up at the right time and right place. The forecast will be based on the weather data of Singapore. 

Data:
The datasets used in this project are number of raining day in a month and total volume of rainfall in a month and 5 other dataset relevant to weather, which are: relative humidity, maximum rainfall in a day, Average air temperature, hourly wet bulb temperature, and Average sunshine hour in a day. In additional to probelm statement, the number of international visitor arrived in Singapore also used.

Deliverables:
Provide a interval of hottest weather period in the day each every month in a year.

Success Criteria:
Success is measured by the model's accuracy in predicting hottest period in the day.



---

## Data import and cleansing

    The data from data.gov.sg are very clean, just need to rename column name to all lower case letter. And change data type of month column to date-time, by using to_datetime from pandas. except for one dataset, the wet_bulb temperature. The wet_bulb temperature is hourly record, where the rest are monthly basis. So in order to make it usable with other dataset, the wet_bulb temperature is grouped by date and the mean is calculated. 

    The additional data used, the number of visitor, has clean data too. This is also indexed as year-month, same as the rest of data. So, just rename the column, changed type, so it can be easily merged with other dataset.

    Next, merge all dataset into single dataframe. The data are then checked for missing values and outliers, fortunately they are none.
    
    The mergeded dataframe and it also has been exported to "processed_data.csv" and located in this repository as well.

---
## Mandatory Questions
### Exploratory Data Analysis

    The merged dataframe is named comb_month. With pandas library, the statistic overall can be calculated easily by function decribe. Or they can also be done by manually calculation or create the function ourselve. 

    To answer the mandatory question. Function to find the highest and lowest value of each variable are created. The function take input of column name and year. The function will return the highest and lowest value of that column in that year. The function is used to answer the question below.


        Q: Which month have the highest and lowest total rainfall in 1990, 2000, 2010 and 2020?
        A:  function is created to find highest and lowest rainfall given input are column name and year
            below are the result: for all question.

            Highest rainfall in 1990 is : 104   1990-09-01
            Lowest rainfall in 1990 is : 97   1990-02-01

            Highest rainfall in 2000 is : 226   2000-11-01
            Lowest rainfall in 2000 is : 224   2000-09-01

            Highest rainfall in 2010 is : 342   2010-07-01
            Lowest rainfall in 2010 is : 337   2010-02-01

            Highest rainfall in 2020 is : 460   2020-05-01
             Lowest rainfall in 2010 is : 337   2010-02-01
           
        Q: Which year have the highest and lowest total rainfall in the date range of analysis?
        A:  Highest rainfall is in year 2007, total rainfall 2,886.2 mm
            Lowest rainfall is in year 1997, total rainfall 1,118.9 mm

        Q: Which month have the highest and lowest number of rainy days in 1990, 2000, 2010 and 2020?
        A:  The function created for first question is usable here as well.
            below are the result: for all question.
            Highest rainfall in 1990 is : 1990-09, 1990-11
            Lowest rainfall in 1990 is : 1990-03

            Highest rainfall in 2000 is : 2000-11
            Lowest rainfall in 2000 is : 2000-04

            Highest rainfall in 2010 is : 2010-11
            Lowest rainfall in 2010 is : 2010-04

            Highest rainfall in 2020 is : 2020-07
             Lowest rainfall in 2010 is : 2010-03

        Q: Which year have the highest and lowest number of rainy days in the date range of analysis?
        A:  Highest rainfall is in year 2013, total rainy days 206
            Lowest rainfall is in year 1997, total rainy days 116

        Q: Are there any outliers months in the dataset?
        A:  I created function to find the upper and lower bound of outliers by inputing column name.
            There are outliers in the dataset
                There are  35 outlier in upper bound of maximum_rainfall_in_a_day
                There are  0 outlier in lower bound of maximum_rainfall_in_a_day
                There are  0 outlier in upper bound of no_of_rainy_daysy
                There are  0 outlier in upper bound of no_of_rainy_daysy
                There are  14 outlier in upper bound of total_rainfall
                There are  0 outlier in lower bound of total_rainfall
                There are  0 outlier in upper bound of mean_rh
                There are  4 outlier in lower bound of mean_rh
                There are  4 outlier in upper bound of mean_sunshine_hrs
                There are  0 outlier in lower bound of mean_sunshine_hrs
                There are  1 outlier in upper bound of temp_mean_daily_min
                There are  0 outlier in lower bound of temp_mean_daily_min
                There are  4 outlier in upper bound of total_visitor
                There are  0 outlier in lower bound of total_visitor
                There are  1 outlier in upper bound of wet_bulb_temperature
                There are  14 outlier in lower bound of wet_bulb_temperature

---
## Data visualization
    - The heat map of coorelation between variables show some degree of relationship, one in particular looks like strong relationship
    Positive correlation (correlation coefficient > 0.5):
        - Total rainfall in a month v.s. Average monthly max rainfall in a day (0.81)
        - Wet bulb temperature v.s. Average air temperature (0.69)
        - Total rainfall in a month v.s. Number of rainy days in a month (0.68)
        - Total rainfall in a month v.s. Average relative humidity in a month (0.59)
        - Number of rainy days in a month v.s. Average relative humidity in a month (0.58)
    Negative correlation (correlation coefficient < -05):
        - Number of sunshine hours in a month v.s. Number of rainy days in a month (-0.68)
        - Average relative humidity in a month v.s. Average air temperature (-0.64)
        - Number of sunshine hours in a month v.s. Average relative humidity in a month (-0.59)
        - Number of sunshine hours in a month v.s. Total rainfall (-0.58)
    
    - Strong correlation reflect in similarity of distribution shape when plot histogram of each variable.

        From the first heatmap, there are 9 pairs of these data where magnitude of correlation coeficient is more than 0.5. The distribution of these data are similar to each other. The pair with right skewed distribution means the mean is greater than the median. This is because the mean is sensitive to outliers and the median is not. The outliers in these data are the months with heavy rain fall. The mean of these data are greater than the median. The distribution of these data are not normal distribution. This will affect the estimate made from these data. for the normal distribution shape, the mean and median and mode are close to each other, makes the average able to represent its true meaning.


    - The processed data contain 488 rows of data (488 months of weather record). Most of them have no outliner, except for the total upper outlier in the total rainfall in a month that looks significant (outlier data is 8% of total dateset). They also confirms the outliers found from filering (masking) data in the previous step.

    - The scatter plot confirms the corelation between variables that found out in heatmap plot ealier

###### Addtional plot and exploration

    - The boxplot for each variable group by 'month' shows the yearly trend, seasonal dimension.
    - It can tell statistically, which month has the highest rain in a year and which month has the lowest rain in a year.
    - Same as number of raining day, it tells the chance of raining in particular month of the year.
    - With wet bulb temperature is the very precise, it has record in hourly basis, so I decided to drill down what can be found.
        - I set up index for each date dimension, year, month, day. Make them numberic, so I can use them to filter easier.
        - Start by finding min and max on each day, by filtering (masking) using groupby function.
        - Then create the list to contain min and max temperature of each day. 
        - By product of this, we can find the frequency which hour of day has the highest temperature or lowest temperature.
        - I can eventually find the hottest time of day in each month of the year.

---

## Finding from analysis
There are some strong correlation amoung variable in datasets. 9 paris of variables has magnitude of correlation coefficient more than 0.5. But they are obvious and expected. for example, correlation coeffiecient between total rainfall in a month and maximum rain fall in a day of particular month. It is obvious because the rainfall is dependency of maximum rainfall in a day.

There are degree of seansonal in term of rainfall in Singapore. Even though Singapore is located in tropical region where the weather is very similar through out the year. But analysis show some degree of seasonal in term of rainfall, sunshine duration, and temperature.

There are no significant pattern channges since 1982. The amount of rainfall, temperature are very much the same today as 40 years ago.

The wet bulb temperature data were recorded by hour. The distribution shape also very close to perfect normal distribution, so mean/median/mode are close to each other. So the statistically analysis rely on mean and standard deviation sufficient to describe the entire distribution
    - Dec, Jan, Feb, and Mar has 50% chances that the hottest time of day will be between noon and 3 pm 
    - Apr, Aug, Oct, and Nov has 50% chances that the hottest time of day will be between 11 am to 3 pm
    - May, Jul, and Sep has 50% chances that the hottest time of day will be between 10 am to 2 pm
    - Jun has 50% chances that the hottest time of day will be between 10am to 3 pm






## Conclusion and Recommendation

February has the best weather for selling ice-cream. It may not be the hottest month, but it has the longest sunlight hour and least chance of raining. 
    
Jun is probably the secord best for uncles. It has the longest hot weather period during the day, and also the hottest month in the year.
    
November and December are the least favorable months for selling ice-cream. They have highest raining chance and the temperature are among the lowest in the year.
    
May, Jul, and Sep are likely to start heating up sooner than others, perhaps uncles need to set up stand earlier than usual.

The rest of the months can be expected to be rained half of the time, with hottest period of the day between 11 am to 3 pm.







