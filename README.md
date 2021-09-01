# Pyber_Analysis

## Overview

Pyber is a python based ride sharing app. In previous analysis, I used python and pandas to examine data from large CSV files (city_data.csv and ride_data.csv). These files contain pyber ridesharing data from urban, suburban, and rural cities. ride_data.csv includes pyber data of specific rides, the cities they occured in, the fare and the ride id number. The city_data_csv included data on each individual city, it's type and it's number of drivers. In the exploratory stage of the analysis, I inspected the data and determined the average ride count, fare, and average number of drivers for each city type. Then, using matplotlib I created visualization of the data, through line graphs, bar graphs, pie graphs, scatter plots and box and whisker plots. This analysis is contained in the pyber.ipynb file which has been uploaded to this repository.  

For the pyber analysis challenge, I am using similar methods to continue analyzing these datasets to create a summary dataframe of the ride sharing data by city type. Then, using pandas and Matplotlib I have created data visualizations that show the average ride fare per week for each type of city. This analysis will show how the data differs by city type and how those differences can be used by decision-makers at PyBer. I will be summarizing my findings below. 

## Analysis

For deliverable 1, I merged the data from both CSV files into one dataframe, called "pyber_data_df". The first five rows of pyber_data_df are shown below.  

<img width="562" alt="Screen Shot 2021-08-31 at 8 16 48 PM" src="https://user-images.githubusercontent.com/84936545/131591995-20b4436a-c537-4cf8-81ad-5226e70ecaab.png">

Using the Pandas groupby() function with the count() and sum() methods on pyber_data_df columns, I calculated the total number of rides, total number of drivers, and the total fares for each city type. Then, I calculated the average fare per ride and average fare per driver for each city type. Finally, I added this data to a new DataFrame and formatted the columns.

<img width="611" alt="Screen Shot 2021-08-30 at 10 52 50 PM" src="https://user-images.githubusercontent.com/84936545/131591409-1ce164fc-dddd-4e16-895a-8620fc685c71.png">

For deliverable 2, I created a multiple-line graph that shows the total fares for each week by city type. To do this I began by Using groupby()to create a new DataFrame showing the sum of the fares for each date where the indices are the city type and date. The code I used and the resulting dataframe are shown below. 

```
new_pyber_data_df = pyber_data_df.groupby(["type", "date"]).sum()[["fare"]]
new_pyber_data_df
```

<img width="236" alt="Screen Shot 2021-08-31 at 8 25 34 PM" src="https://user-images.githubusercontent.com/84936545/131592569-80c9de1e-210c-4068-9bdd-65a098aabcb2.png">

Next, after resetting the index I created a pivot table dataframe with the 'date' as the index, the columns ='type', and values='fare' to get the total fares for each type of city by the date. The code I used and resulting pivot table dataframe are below. 
```
new_pyber_data_df = new_pyber_data_df.pivot(index='date', columns='type', values='fare')
new_pyber_data_df
```
<img width="302" alt="Screen Shot 2021-08-31 at 8 33 18 PM" src="https://user-images.githubusercontent.com/84936545/131593128-9dff9790-dd0c-4dfb-99fa-33067ec6a737.png">

Next, I created a new DataFrame from the pivot table DataFrame using loc on the given dates, '2019-01-01':'2019-04-29'. I made sure to set the "date" index to datetime datatype using the following code. The resulting dataframe is below.  

```
new_pyber_data_df.index = pd.to_datetime(new_pyber_data_df.index)
```

<img width="311" alt="Screen Shot 2021-08-31 at 8 40 03 PM" src="https://user-images.githubusercontent.com/84936545/131593540-2e9d37fc-e4aa-4932-a6dd-f9731d4ffdd6.png">

For the final dataframe I used the resample() function by week 'W' to get the sum of the fares for each week. The code and dataframe are displayed below. 

```
pyber_week_data_df = new_pyber_data_df.resample('W').sum()
pyber_week_data_df.head()
```

<img width="262" alt="Screen Shot 2021-08-31 at 8 42 15 PM" src="https://user-images.githubusercontent.com/84936545/131593742-96ff164f-5d81-4326-a5c6-5b1dc2e7524b.png">

To visualize the data, I graphed the resampled DataFrame using the df.plot() method, as well as the Matplotlib "fivethirtyeight" graph style.  

```
# Import the style from Matplotlib.
from matplotlib import style

style.use('fivethirtyeight')
pyber_week_data_df.plot(linewidth=1, figsize=(13, 5))
plt.xlabel('Month')
plt.ylabel('Fare')
plt.title("Total Fare by City Type")
```

The resulting graph is below. 

<img width="915" alt="Screen Shot 2021-08-31 at 8 48 03 PM" src="https://user-images.githubusercontent.com/84936545/131594146-553d6ec3-be8c-41c5-85b8-1a3387a750fe.png">

The Y axis displays the average fare(in US$) and the X axis displays the week in which it occured. 

## Results

Results by city type: 

Urban: 
* Total rides: 1625
* Total drivers: 2405 
* Total fares: 39,854.38$
* Average fare per ride: 24.53$
* Average fare per driver: 16.57$

Suburban: 
* Total rides: 625
* Total drivers: 490 
* Total fares: 19,356.33$
* Average fare per ride: 30.97$
* Average fare per driver: 39.50$

Rural: 
* Total rides: 125
* Total drivers: 78
* Total fares: 4327.93$
* Average fare per ride: 34.62$
* Average fare per driver: 44.49$


## Recommendations 




