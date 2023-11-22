# Data Science & Machine Learning Portfolio

## Overview

This repository displays my data science and machine learning projects, highlighting my skills in data management, programming, and creating machine learning models.

### Table of Contents

1. [Introduction](#introduction)
2. [Background](#background)
3. [About Me](#about-me)
4. [Project Portfolio](#project-portfolio)
   - [Project 1: Daytime Heart Rate Insights to Predict Sleep Stages with Fitbit Data](#project-1-Daytime-Heart-Rate-Insights-to-Predict-Sleep-Stages-with-Fitbit-Data)
   - [Project 2: Predictive Analysis of Road Fatalities in Ireland](#project-2-predictive-analysis-of-road-fatalities-in-ireland)
   - [Project 3: Rugby World Cup (RWC) Match Outcome Predictions & Player Statistics](#project-3-rugby-world-cup-match-outcome-predictions-&-player-statistics)
5. [All Technologies Used](#all-technologies-used)
6. [How to Run](#how-to-run)
7. [Portfolio Specification](#portfolio-specification)
8. [Contributors](#contributors)

## Introduction

In this repository, you will find a collection of data science and machine learning projects that I have worked on during my academic journey. These projects demonstrate my skills and expertise in various areas of data science and machine learning, including data analysis, data visualization, model development, and more.

## Background

In this section, you would:

- **Significance of the Portfolio**: Explain why showcasing your projects is essential. This could relate to demonstrating understanding in modern tools and techniques.

- **Purpose**: Describe what readers should expect from the portfolio.

## About Me
   ### Profile
   - **Name:** Conor Brooke 
   - **Academic Qualifications:** Bachelor of Science in Software Development 
   
   ### Contact Information
   - **Email:** c00260735@setu.ie
   - **GitHub:** [GitHub Profile](https://github.com/conorbrooke77)


## Project Portfolio

## Project 1: Daytime Heart Rate Insights to Predict Sleep Stages with Fitbit Data

### Description

This project aims to predict sleep stages using data from Fitbit wearables. The Fitbit dataset contains records of 30 participants, capturing metrics such as heart rate recorded every second, sleep metrics, and step metrics. A key focus of this study is to analyze heart rate variations throughout the day and its potential impact on sleep stages. By understanding how heart rate fluctuates during different times of the day, this project tries to find patterns that might inform the quality of rest a person gets at night. The idea is that elevating your heart rate at certain times during the day could potentially lead to better rest during the night.

The FitBit Fitness Tracker Data datasets were generated by respondents to a distributed survey via Amazon Mechanical Turk between 03.12.2016-05.12.2016. All data discussed below represents these 30 participants over this two-month period. The project also aims to explore the individual differences in heart rate and sleep patterns, providing insights into personalized strategies for optimizing rest.

### Dataset
**FitBit Fitness Tracker Data:** [Kaggle](https://www.kaggle.com/datasets/arashnic/fitbit/data)

Below are the total rows of each dataset used:  

`heartrate_seconds_num_rows = 2483658`  

`minuteSleep_num_rows = 188521`  

`minuteSteps_num_rows= 1325580`  
    
### Technologies Used
- Python
- Pandas
- Matplotlib (for visualization) 
- Numpy

### Techniques Applied and How They Were Used

#### 1. Data Cleaning and Preprocessing

- **Null Value and Data Type Check**
    ```python
    # Checked for any Null values and inconsistent datatypes across all datasets
    ```

- **Datetime Formatting**
    ```python
    minuteSleep['date'] = pd.to_datetime(minuteSleep['date'], format='%m/%d/%Y %I:%M:%S %p')
    heartrate_seconds['Time'] = pd.to_datetime(heartrate_seconds['Time'], format='%m/%d/%Y %I:%M:%S %p')
    minuteSteps['ActivityMinute'] = pd.to_datetime(minuteSteps['ActivityMinute'], format='%m/%d/%Y %I:%M:%S %p')
    ```
    Datetime columns were converted to a consistent format for easier handling and manipulation.

- **Column Renaming**
    ```python
    heartrate_seconds.rename(columns={'Time': 'date'}, inplace=True)
    minuteSteps.rename(columns={'ActivityMinute': 'date'}, inplace=True)
    heartrate_seconds.rename(columns={'Value': 'Heart Rate'}, inplace=True)
    minuteSleep.rename(columns={'value': 'SleepStage'}, inplace=True)
    ```
    Columns were renamed to maintain consistency and clarity across datasets.

- **Column Removal**
    ```python
    minuteSleep.drop(columns=['logId'], inplace=True)
    ```

- **Data Resampling**
    ```python
    heartrate_minutes = (
        heartrate_seconds
        .groupby(['Id', heartrate_seconds['date'].dt.floor('T')]) 
        .agg({'Heart Rate': 'mean'})
        .reset_index()
    )
    ```
    Heart rate data was resampled from seconds to minutes granularity to reduce dataset size and improve manageability.

#### 2. Exploratory Data Analysis (EDA)

- **Visualization of Heart Rate Data Per Hour Over a Month Period**
    ```python
    plt.figure(figsize=(15, 7))
    for individual in sampled_individuals:
        individual_data = hourly_data[hourly_data['Names'] == individual]
        plt.plot(pd.to_datetime(individual_data['Date'].astype(str) + ' ' + individual_data['Hour'].astype(str) + ':00:00'), 
                 individual_data['Avg Heart Rate Per Minute'], 
                 label=individual)
    ```
    This code was used to generate a visualization showcasing the average heart rate per hour for randomly sampled individuals.

    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Resources/Average%20Heart%20Rate%20Per%20Hour%20for%20Sampled%20Individuals.png?raw=true)  

    **Basic Statistical Summary for Sampled Individuals:**

    Mean (Average) Heart Rate: 69.52 beats per minute  
    Standard Deviation: 15.19  
    Minimum Heart Rate: 36.8 beats per minute  
    Maximum Heart Rate: 187.0 beats per minute  
    Median (50th percentile) Heart Rate: 66.43 beats per minute  
    25th Percentile: 59.40 beats per minute  
    75th Percentile: 75.80 beats per minute  

- **Visualization of Heart Rate Data Per Hour For A Sample User**
    ```python
    # Filter for a specific date for Joe
    specific_date = "2016-04-13"
    joe_data = hourly_data[(hourly_data['Names'] == 'Joe') & (hourly_data['Date'] == specific_date)]

    # Plotting the data for Joe
    plt.figure(figsize=(15, 7))
    plt.plot(pd.to_datetime(joe_data['Date'].astype(str) + ' ' + joe_data['Hour'].astype(str) + ':00:00'), 
    joe_data['Avg Heart Rate Per Minute'], 
    label='Joe', color='blue')
    ```
    This code was used to generate a visualization showcasing the average heart rate per hour for randomly sampled individuals.

    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Resources/Joe%20Daily%20Heart%20Rate%20analysis.png?raw=true)  

    **Basic Statistical Summary for Joe on 2016-04-13:**

    Mean (Average) Heart Rate: 60.59 beats per minute  
    Standard Deviation: 4.33  
    Minimum Heart Rate: 51.77 beats per minute  
    Maximum Heart Rate: 68.47 beats per minute  
    Median (50th percentile) Heart Rate: 61.51 beats per minute  
    25th Percentile: 57.65 beats per minute  
    75th Percentile: 63.30 beats per minute  

- **Visualization of Sleep Stages Distribution**
    ```python
    total_minutes_per_stage = sleep_duration.groupby('SleepStage')['Duration_minutes'].sum()
    total_minutes = total_minutes_per_stage.sum()
    percentage_per_stage = (total_minutes_per_stage / total_minutes) * 100
    percentage_per_stage.plot(kind='bar', color=['blue', 'green', 'red'])
    plt.title('Percentage of Time Spent in Each Sleep Stage')
    plt.ylabel('Percentage (%)')
    plt.xlabel('Sleep Stage')
    plt.show()
    ```
    This code was used to generate a visualization of Sleep Stages Distribution. The data is highly unlikely and may be inaccurate.

    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Resources/sleep-stage-data.png?raw=true)  


#### 3. Feature Engineering

- **Time Data Splitting**
    ```python
    heartrate_minutes_split_time = heartrate_minutes['DateTime'].str.split(' ', expand=True)
    ```
    The DateTime column was split into separate date and time components for more granular analysis.

- **Usernames Association**
    ```python
    heartrate_minutes['Names'] = heartrate_minutes['Id'].map(id_to_name)
    ```
    Random names were associated with user IDs for clearer and more human-readable data visualization.

- **Sleep Stage Mapping for Readability**
    ```python
    sleep_stages = {
        1: 'Awake',
        2: 'REM',
        3: 'Deep Sleep'
    }
    # Apply the mapping to the 'SleepStage' column
    minuteSleep['SleepStage'] = minuteSleep['SleepStage'].replace(sleep_stages)
    ```

- **Calculating Sleep Duration per Sleep Stage**
    ```python
    minuteSleepCopy['day'] = minuteSleepCopy['date'].dt.date
    sleep_duration = minuteSleepCopy.groupby(['Id', 'day', 'SleepStage']).size().reset_index(name='Duration_minutes')
    ```
    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Resources/Daily-SleepDuration.png?raw=true) 

- **Understanding Sleep Data Consistency**
    ```python
    total_sleep = minuteSleepCopy.groupby(['Id', 'day']).size().reset_index(name='Total_minutes')
    # Merge total_sleep with sleep_duration
    sleep_duration = sleep_duration.merge(total_sleep, on=['Id', 'day'])
    # Calculate the percentage
    sleep_duration['Percentage'] = (sleep_duration['Duration_minutes'] / sleep_duration['Total_minutes']) * 100
    ```
    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Resources/Percentage-Sleep.png?raw=true)  

    Completely inaccurate or misunderstood data, as its highly unlikely to stay awake 94% of each day for a month.
    FitBit gives a better breakdown of how nighttime sleep pattern distrubution should look: [FitBit](https://blog.fitbit.com/sleep-stages-explained/)


### Data Processing Techniques

The data, sourced from Fitbit (Fitabase), presented potential biases due to its limitation to 30 participants. The third-party nature of the collection method further raised issues. Addressing these challenges required several processing techniques:

- Datetime formatting was changed for consistency.
- Heart rate data had to be resampling to a minute granularity, reducing the dataset's size for manageability.
- Feature engineering split date and time for clearer time-series data interpretation.
- Data cleaning saw the removal of non-essential columns and renaming for clarity e.g, logid column which had inconsistent data and didn't correlate across datasets.

### Opportunities from the Project

- Delve into the relationship between heart rate and sleep stages, offering insights into potential sleep stage predictions using Fitbit data.
- Acquire hands-on experience with real-world datasets.
- Improve understanding of time-series data.

### New Technologies Learned

- Practice with Pandas for data preprocessing and exploratory data analysis.
- Visualization techniques, particularly with Matplotlib.

### Datasets Explored

- **heartrate_seconds**: Captured heart rates every second.
- **minuteSleep**: Documented sleep metrics every minute.
- **minuteSteps**: Recorded steps metrics every minute.

### Skills Acquired

- Better understanding of time-series data analysis.
- Basic skills in data cleaning.
- Feature engineering within date-time data.
- Practise with visualization of time-series data.

### Challenges Faced

- Merging posed challenges due to the extensive dataset sizes, had many problems finding ways to merge data beneficially while staying coherent.
- Due to merging challenges and the limited number of participants, establishing a connection between the heart rate and sleep stages data proved to be incredibly frustrating.
- The MinuteSleep data was hard to differentiate between daytime and nighttime hours, making it either inaccurate or I struggled to interpret it correctly.
- Formatting on the steps data was also a challenge to interpret, along with having what seemed like a pointless column.
- Differing granularities between datasets causing resampling of datasets.
- The dataset's potential biases came from a limited participant count and third-party collection methods, eventhough datasets are large the data stays quite consistent.
- The MinuteSleep data, based on the percentage analysis, is inconsistent and inaccurate. This has led to challenges in interpreting the data correctly.
- In-depth analysis of sleep stages showed that users spent an unusually high percentage of time being "Awake", raising concerns about the reliability of this dataset.

### Modeling Roadblocks

Haven't begun modeling for Iteration 1.

### Conceptual Hurdles

- Have to get a better grasp on the aspects influencing sleep stages.
- Understading the relationship between heart rate and sleep aswell as physical activity on sleep, especially considering the inconsistencies present in the sleep data.

### Disappointing Conclusion

I tried to use Fitbit data to understand sleep patterns. But I ran into problems.
The main issue was with the `minuteSleep` dataset. It didn't seem right. For example, it showed that users were "Awake" a lot more than expected. This makes us question if the data is good or not. The `minuteSteps` dataset also didn't have enough useful data to re-orintate the goal to a prediction using physical activity.
Because of these issues, I might need to change my approach. Maybe I'll look at the data hour by hour next time. Or use a totally different dataset.
Even though I faced challenges, I learned a lot. I found out how important it is to double-check my data. I hope to find better dataset for the second iteration.

<br>
<br>
<br>
<br>
  
## Project 2: Predictive Analysis of Road Fatalities in Ireland 

#### Temporary Explaination For Starting New Project
*I understand that 'Iteration 2' is intended to build upon 'Iteration 1', however, issues and inconsistencies within the datasets used in the initial project has prevented any conclusive findings for predicting sleep stages for Fitbit wearables.*
  
*So instead, I have started a new project entirely with 'Iteration 2'. This revised project not only include the completion of the techniques from 'Iteration 1',but also develops on these techniques with improved findings. Also the project you provided on decision trees and random forests will now be included as Project 3 instead of Project 2.*

### Description
This project revolves around the issue of road safety, aiming to analyse each dataset and develop a model to predict road fatalities in Ireland. The datasets were gathered from the Central Statistics Office of Ireland under the Road Safety Statistics data table. Combined accross both datasets is the road fatality data that spans from January 2000 to October 2023, the objective is to find patterns and trends that can help estimate future road fatality in Ireland. 

The two datasets used in this project are ROA11 and ROA29, by analysing this data, a predictive model in road fatalities can be developed. The project will implement techniques like data cleaning and preprocessing, making sure the data is ready for analysis. This will also be followed by feature engineering and exploratory data analysis (EDA), where the data will be further analysed and engineered.

The predictive model developed will be expected to use the SARIMA approach, a statistical model used to forecast future values by including non-seasonal and seasonal trends. This method is well suited for the time series data of the ROA11 and ROA29 datasets. The project's expected outcome is a model based on analyse of Irelands road fatalities that could help improve road safety planning. This project's audience is for anyone wanting to make a difference using data, including policymakers, road safety analysts, or the Irish public interested in road safety trends.


### Datasets Discussed
*Check the Dataset out yourself:* [Road Safety Statistics](https://data.cso.ie/product/RSARS)
<br>
<br>
    
#### Renaming Datasets for Clarity in Python

This section of the code focuses on renaming the datasets used from Road Safety Statistics (ROA11 and ROA29) to improve clarity.
```python
# Includes annual road fatalities with a breakdown by month (2000 - 2023 September)
road_fatalities_monthly = pd.read_csv("ROA11.20231122T121139.csv")

# Contains most up-to-date monthly road fatalities in Ireland (2000 January - 2023 October)
current_road_fatalities_monthly = pd.read_csv("ROA29.20231122T121128.csv")
```
#### Below are the total rows of each dataset used:  

`total_rows_road_fatalities_monthly = 312`  

`total_rows_current_road_fatalities_monthly = 286`  
    <br>  
    
### Technologies Used
- Python: For programming, analysis, and modeling.
- Pandas: For dataset manipulation.
- Matplotlib: For data visualization and EDA.
- Scikit-learn: For implementing machine learning models.
- Jupyter Notebook: As the development environment.
<br>
<br>

### Techniques Applied and How They Were Used

#### 1. Data Cleaning and Preprocessing

- **Identify and Removal of Null Values**  
  
   ```python
   print("Null Values:\n", road_fatalities_monthly.isnull().sum())
   print("Null Values:\n", current_road_fatalities_monthly.isnull().sum())
   road_fatalities_monthly.dropna(inplace=True)
   ```
<br>

In the `road_fatalities_monthly` dataset, I found 3 missing values in the 'VALUE' column, unlike the `current_road_fatalities_monthly` dataset, which is complete with no missing values. I removed the rows with   null values in `road_fatalities_monthly` and will retrieve this missing data when combining datasets.
<br>
<br>

- **Column Removal and Renaming**
    ```python
   road_fatalities_monthly.rename(columns={'VALUE': 'Road Fatality Count'}, inplace=True)
   road_fatalities_monthly.rename(columns={'Month of Fatality': 'Month'}, inplace=True)
   road_fatalities_monthly.drop(columns=['UNIT', 'STATISTIC Label'], inplace=True)
   
   current_road_fatalities_monthly.rename(columns={'VALUE': 'Road Fatality Count'}, inplace=True)
   current_road_fatalities_monthly.drop(columns=['UNIT', 'Statistic Label', 'Ireland'], inplace=True)
    ```
<br>
<br>

The datasets 'VALUE' column names were modified for better clarity which is essential for analysis. The 'Month of Fatality' column in `road_fatalities_monthly` was also renamed to 'Month'.
By dropping the columns 'UNIT', 'Statistic Label', and 'Ireland', it focuses the datasets on only relevant information, making the data easier to understand and analyze.
<br>
<br>

- **Merging Road Fatality Datasets for Improved Analysis**
  
  ```python
   current_road_fatalities_monthly[['Year', 'Month']] = current_road_fatalities_monthly['Month'].str.split(' ')
   current_road_fatalities_monthly['Year'] = current_road_fatalities_monthly['Year'].astype(int)
  ```
<br>
<br>
By splitting the 'Month' column into separate 'Month' and 'Year' columns, both dataset columns are aligned, allowing easier merging and comparison across datasets.
<br>
<br>  

  ```python
   road_fatalities_2000_to_2023 = pd.concat([temp_current_road_fatalities_monthly, all_months_data], ignore_index=True)

   road_fatalities_2000_to_2023 = road_fatalities_2000_to_2023.drop(road_fatalities_2000_to_2023.index[-1])
  ```
<br>
<br>
Both datasets are now merged into one dataset `road_fatalities_2000_to_2023`, with a new value 'Annual Summary' at the end of each year. The 'Annual Summary' for 2023 is removed as the year hasn't ended.
<br>
<br> 

**Merged Road Fatalities Dataset**  
<br> 
   ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Resources/Dataset_After_Merge.png) 
<br>
<br>   
      
#### 2. Feature Engineering

- **Mapping Seasons To The Dataset**
    ```python
    # Mapping each month to its season
    seasons = {
       'January': 'Winter', 'February': 'Winter', 'March': 'Spring',
       'April': 'Spring', 'May': 'Spring', 'June': 'Summer',
       'July': 'Summer', 'August': 'Summer', 'September': 'Autumn',
       'October': 'Autumn', 'November': 'Autumn', 'December': 'Winter',
       'Annual Fatalities': 'Annual'
   }

   # Creating a new column 'Season'
   road_fatalities_2000_to_2023['Season'] = road_fatalities_2000_to_2023['Month'].map(seasons)
    ```
<br>
<br>

Including a 'Season' column in the dataset provides insights into seasonal changes in road fatalities. It allows for the analysis of trends and patterns that may differ across seasons due to varying weather conditions, daylight hours, and driving behaviors.
<br>
<br>

**Road Fatalities Dataset With Season Column**  
   ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Resources/Seasons_Added.png)  
   
<br>
<br>

#### 3. Exploratory Data Analysis (EDA)

- **Visualization of Yearly Road Fatalities in Ireland (2000 - 2022)**
    ```python
   # Selecting only the 'Year' and 'Road Fatality Count' columns for plotting
   annual_road_fatalities = annual_road_fatalities[['Year', 'Road Fatality Count']].set_index('Year')
   
   plt.figure(figsize=(14, 7))
   
   # Giving a marker for each year
   annual_road_fatalities['Road Fatality Count'].plot(kind='line', marker='o')
   plt.title('Yearly Trend of Road Fatalities in Ireland (2000 - 2023)')
   plt.xlabel('Year')
   plt.ylabel('Number of Fatalities')
   plt.grid(True)
   plt.show()
    ```
   This code was used to generate a visualization showcasing the Yearly Trend of Road Fatalities in Ireland (2000 - 2022).
<br>

   ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Resources/Yearly-Trend-of-Road-Fatalities-in-Ireland-2022.png)  
<br>

   **Statistical Summary of Yearly Road Fatalities (2000 - 2022)**
  
   Mean Fatalities (Average): 246.87  
   Standard Deviation: 103.29  
   Minimum Fatalities: 135.0  
   25th Percentile: 158.5  
   Median: 192.0  
   75th Percentile: 351.5  
   Maximum Fatalities: 415.0

<br>

- **Visualization of Yearly Trend of Road Fatalities in Ireland after 2006**
    ```python
   specific_road_fatalities = road_fatalities_2000_to_2023[(road_fatalities_2000_to_2023['Month'] == 'Annual Fatalities')
                                                          & (road_fatalities_2000_to_2023['Year'] > 2006)]
   
   # Selecting only the 'Year' and 'Road Fatality Count' columns for plotting
   specific_road_fatalities = specific_road_fatalities[['Year', 'Road Fatality Count']].set_index('Year')
   
   plt.figure(figsize=(14, 7))
   
   # Giving a marker for each year
   specific_road_fatalities['Road Fatality Count'].plot(kind='line', marker='o')
   plt.title('Trend of Road Fatalities in Ireland after RSA was formed')
   plt.xlabel('Year')
   plt.ylabel('Number of Fatalities')
   plt.grid(True)
   plt.show()
    ```
   This code was used to generate a visualization showcasing the Yearly Trend of Road Fatalities in Ireland (2006 - 2023).
<br>

   ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Resources/Yearly-Trend-of-Road-Fatalities-in-Ireland_2006.png)  
<br>
<br>

   **Statistical Summary of Road Fatalities after 2006**
  
   Mean (Average): 187.88  
   Standard Deviation: 56.00  
   Minimum: 135.0  
   25th Percentile: 152.0  
   Median (50th Percentile): 172.5  
   75th Percentile: 197.0  
   Maximum: 338.0  
<br>

**Annual Data Trends Analysis**  

<br>
The yearly trend of road fatalities in Ireland, as shown in the first plot graph, reveals a major decline in fatalities from 2000 to 2022. Starting at 415 fatalities in 2000, there has been a general downward trend, reaching as low as 135 in recent years. 
This decrease could be due to many factors:<br><br>

**Enhanced Road Safety Measures:** Over the years, Ireland has implemented more effective road safety policies, including stricter enforcement of traffic laws, improved road infrastructure, and better safety awareness campaigns like Road Safety Authority (RSA) formed in 2006.<br><br>
**Improvement in Vehicle Safety:** Modern vehicles are equipped with better safety features like anti-lock braking systems, and electronic stability control.<br><br>
**Driver Behaviour Changes:** There is a correlation between RSA being formed and a major drop in road fatalities as shown in the second graph. RSA could have helped raise awareness on driving safety in Ireland, which has positively influenced driving safety, leading to safer roads.<br><br>
The mean data shown in the second graph indicates on average a decrease in 60 fatalities annually on Irish roads after 2006. The analysis suggests that future road safety initiatives could continue this positive trend, further reducing fatalities on Ireland's roads.

<br>

- **Visualization of Seasonal Impact on Road Fatalities in Ireland (2000 - 2023)**
    ```python
   seasonal_fatalities = filtered_data.groupby('Season')['Road Fatality Count'].sum()
   
   plt.figure(figsize=(10, 6))
   sns.barplot(x=seasonal_fatalities.index, y=seasonal_fatalities.values)
    ```
   This code was used to generate a visualization showcasing the Seasonal Impact on Road Fatalities in Ireland (2000 - 2023).
<br>

   ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Resources/Seasonal-Trend-of-Road-Fatalities-in-Ireland-2022.png)  
<br>
<br>

   **Seasonal Statistics of Road Fatalities in Ireland (2000 - 2023)**
   Mean (Average): 1459.00  
   Standard Deviation: 55.97  
   Minimum: 1399.0  
   25th Percentile: 1434.25  
   Median (50th Percentile): 1451.5  
   75th Percentile: 1476.25  
   Maximum: 1534.0    
<br>

**Seasonal Trends Analysis**  

<br>
The seasonal bar chart shows a consistent range of road fatalities in Ireland from 2000 to 2023, with a mean of 1459. The standard deviation of 55.97 suggests moderate variability within seasons. This stability in seasonal patterns could be crucial for predicting future trends for road fatalities in Ireland.

<br>
   
<br>
<br>

### Data Processing Techniques

The data, sourced from Fitbit (Fitabase), presented potential biases due to its limitation to 30 participants. The third-party nature of the collection method further raised issues. Addressing these challenges required several processing techniques:

- Datetime formatting was changed for consistency.
- Heart rate data had to be resampling to a minute granularity, reducing the dataset's size for manageability.
- Feature engineering split date and time for clearer time-series data interpretation.
- Data cleaning saw the removal of non-essential columns and renaming for clarity e.g, logid column which had inconsistent data and didn't correlate across datasets.

### Opportunities from the Project

- Delve into the relationship between heart rate and sleep stages, offering insights into potential sleep stage predictions using Fitbit data.
- Acquire hands-on experience with real-world datasets.
- Improve understanding of time-series data.

### New Technologies Learned

- Practice with Pandas for data preprocessing and exploratory data analysis.
- Visualization techniques, particularly with Matplotlib.

### Datasets Explored

- **heartrate_seconds**: Captured heart rates every second.
- **minuteSleep**: Documented sleep metrics every minute.
- **minuteSteps**: Recorded steps metrics every minute.

### Skills Acquired

- Better understanding of time-series data analysis.
- Basic skills in data cleaning.
- Feature engineering within date-time data.
- Practise with visualization of time-series data.

### Challenges Faced

- Merging posed challenges due to the extensive dataset sizes, had many problems finding ways to merge data beneficially while staying coherent.
- Due to merging challenges and the limited number of participants, establishing a connection between the heart rate and sleep stages data proved to be incredibly frustrating.
- The MinuteSleep data was hard to differentiate between daytime and nighttime hours, making it either inaccurate or I struggled to interpret it correctly.
- Formatting on the steps data was also a challenge to interpret, along with having what seemed like a pointless column.
- Differing granularities between datasets causing resampling of datasets.
- The dataset's potential biases came from a limited participant count and third-party collection methods, eventhough datasets are large the data stays quite consistent.
- The MinuteSleep data, based on the percentage analysis, is inconsistent and inaccurate. This has led to challenges in interpreting the data correctly.
- In-depth analysis of sleep stages showed that users spent an unusually high percentage of time being "Awake", raising concerns about the reliability of this dataset.

### Modeling Roadblocks

Haven't begun modeling for Iteration 1.

### Conceptual Hurdles

- Have to get a better grasp on the aspects influencing sleep stages.
- Understading the relationship between heart rate and sleep aswell as physical activity on sleep, especially considering the inconsistencies present in the sleep data.

### Conclusion

I tried to use Fitbit data to understand sleep patterns. But I ran into problems.
The main issue was with the `minuteSleep` dataset. It didn't seem right. For example, it showed that users were "Awake" a lot more than expected. This makes us question if the data is good or not. The `minuteSteps` dataset also didn't have enough useful data to re-orintate the goal to a prediction using physical activity.
Because of these issues, I might need to change my approach. Maybe I'll look at the data hour by hour next time. Or use a totally different dataset.
Even though I faced challenges, I learned a lot. I found out how important it is to double-check my data. I hope to find better dataset for the second iteration.


### Project 3: Rugby World Cup Match Outcome Predictions & Player Statistics

- **Description**: A brief description of the project.
- **GitHub Repository**: [Link to GitHub Repo](https://github.com/conorbrooke77/Data-Science-ML-Project)
- **Live Demo**: [Link to Live Demo](https://www.youtube.com/)
- **Technologies Used**: Examples: Python, Scikit-Learn, Pandas, BeautifulSoup (for web scraping).
- **Techniques Applied**: 
  - **Data Processing Techniques**: E.g., normalization, encoding, etc.
- **Opportunities from the Project**: 
  - **New Technologies Learned**: Briefly mention new tools, frameworks, or libraries you explored during the project.
  - **Datasets Explored**: Discuss any unique or challenging datasets you worked with.
  - **Skills Acquired**: Highlight any particular skills or concepts you learned or refined during the project.

- **Challenges Faced**: 
  - **Data Challenges**: Discuss issues related to data quality, imbalances, missing values, etc.
  - **Modeling Roadblocks**: Highlight any difficulties in model selection, training, or performance.
  - **Implementation Barriers**: Mention if there were any challenges in integrating your model with applications or other systems.
  - **Conceptual Hurdles**: Describe any conceptual challenges you encountered and how you overcame them.

- **Sample Screenshots**:
  Below are sample visualizations generated from the project:  <br>
  <br>
  <img src="https://images.theconversation.com/files/545652/original/file-20230830-15-fd91hb.png?ixlib=rb-1.1.0&q=45&auto=format&w=1000&fit=clip" alt="Visualization1" width="380" height="250">
  <img src="https://images.theconversation.com/files/545680/original/file-20230831-19-uxyx75.png?ixlib=rb-1.1.0&q=45&auto=format&w=1000&fit=clip" alt="Visualization2" width="380" height="250">
  
- **Ethical Considerations**: 
  Describe any ethical concerns you had while working on the project data. Consider aspects like bias, fairness, or implications of predictive outcomes.

- **Regulations and Compliance**:
  - **GDPR Compliance**: Discuss how you ensured that the data handling and processing complied with GDPR regulations.

## All Technologies Used

- List the key technologies and tools you have used in your projects.

## How to Run

Provide instructions on how to run the projects locally if applicable.

## Portfolio Specification

- [Portfolio Specification Document](link-to-specification-document.pdf)

## Contributors

- [Conor Brooke](https://github.com/conorbrooke77) - Main contributor

