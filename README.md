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

    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Average%20Heart%20Rate%20Per%20Hour%20for%20Sampled%20Individuals.png?raw=true)  

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

    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Joe%20Daily%20Heart%20Rate%20analysis.png?raw=true)  

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

    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/sleep-stage-data.png?raw=true)  


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
    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Daily-SleepDuration.png?raw=true) 

- **Understanding Sleep Data Consistency**
    ```python
    total_sleep = minuteSleepCopy.groupby(['Id', 'day']).size().reset_index(name='Total_minutes')
    # Merge total_sleep with sleep_duration
    sleep_duration = sleep_duration.merge(total_sleep, on=['Id', 'day'])
    # Calculate the percentage
    sleep_duration['Percentage'] = (sleep_duration['Duration_minutes'] / sleep_duration['Total_minutes']) * 100
    ```
    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Percentage-Sleep.png?raw=true)  

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
<br>
*So instead, I have started a new project entirely with 'Iteration 2'. This revised project not only include the completion of the techniques from 'Iteration 1',but also develops on these techniques with improved findings. Also the project you provided on decision trees and random forests will now be included as Project 3 instead of Project 2.*

### Description
This project revolves around the issue of road safety, aiming to develop a model to predict road fatalities in Ireland. The datasets were gathered from the Central Statistics Office of Ireland under the Road Safety Statistics data table. Both datasets provide road fatality data that spans from January 2000 to October 2023, the objective is to find patterns and trends that can help estimate future road fatality in Ireland this year.  

The two datasets used in this project are ROA11 and ROA29, which include records of road fatalities in Ireland over the last two decades. By analysing this data, a predictive model to find seasonal trends in road fatalities can be developed. The project will implement techniques like data cleaning and preprocessing, making sure the data is ready for analysis. This will also be followed by exploratory data analysis (EDA), where the data will be further analysed to discover all trends and patterns.  

The predictive model developed will be expected to use the SARIMA approach, a statistical model used to forecast future values by including non-seasonal and seasonal trends. This method is well suited for the time series data of the ROA11 and ROA29 datasets. The project's expected outcome is a model that can predict road fatalities accurately for the remainder of 2023, helping to improve road safety planning for this winter. This project's audience is for anyone wanting to make a difference using data, including policymakers, road safety analysts, or the Irish public interested in road safety trends.


### Datasets Discussed
*Check the Dataset out yourself:* [Road Safety Statistics](https://data.cso.ie/product/RSARS)

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

    
### Technologies Used
- Python: For programming, analysis, and modeling.
- Pandas: For dataset manipulation.
- Matplotlib: For data visualization and EDA.
- Scikit-learn: For implementing machine learning models.
- Jupyter Notebook: As the development environment.

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

    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Average%20Heart%20Rate%20Per%20Hour%20for%20Sampled%20Individuals.png?raw=true)  

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

    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Joe%20Daily%20Heart%20Rate%20analysis.png?raw=true)  

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

    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/sleep-stage-data.png?raw=true)  


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
    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Daily-SleepDuration.png?raw=true) 

- **Understanding Sleep Data Consistency**
    ```python
    total_sleep = minuteSleepCopy.groupby(['Id', 'day']).size().reset_index(name='Total_minutes')
    # Merge total_sleep with sleep_duration
    sleep_duration = sleep_duration.merge(total_sleep, on=['Id', 'day'])
    # Calculate the percentage
    sleep_duration['Percentage'] = (sleep_duration['Duration_minutes'] / sleep_duration['Total_minutes']) * 100
    ```
    ![alt text](https://github.com/conorbrooke77/Data-Science-ML-Project/blob/main/Percentage-Sleep.png?raw=true)  

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

