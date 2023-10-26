# Data Science & Machine Learning Portfolio

## Overview

This repository displays my data science and machine learning projects, highlighting my skills in data management, programming, and creating machine learning models.

### Table of Contents

1. [Introduction](#introduction)
2. [Background](#background)
3. [About Me](#about-me)
4. [Project Portfolio](#project-portfolio)
   - [Project 1: Predictive Analysis on Healthcare Data](#project-1-predictive-analysis-on-healthcare-data)
   - [Project 2: Real-time Tweet Sentiment Analysis](#project-2-real-time-tweet-sentiment-analysis)
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

## Project 1: Predicting Sleep Stages using Fitbit Data

### Description

This project aims to predict sleep stages using data from Fitbit wearables. The Fitbit dataset contains records of 30 participants, including metrics like heart rate recorded every second, sleep metrics recorded every minute, and steps metrics. This study focuses on analyzing the heart rate and its relation to sleep stages to make effective predictions.

### Technologies Used
- Python
- Pandas
- Matplotlib (for visualization)

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

- **Visualization of Heart Rate Data**
    ```python
    plt.figure(figsize=(15, 7))
    for individual in sampled_individuals:
        individual_data = hourly_data[hourly_data['Names'] == individual]
        plt.plot(pd.to_datetime(individual_data['Date'].astype(str) + ' ' + individual_data['Hour'].astype(str) + ':00:00'), 
                 individual_data['Avg Heart Rate Per Minute'], 
                 label=individual)
    ```
    This code was used to generate a visualization showcasing the average heart rate per hour for randomly sampled individuals.

    *INSERT VISUALIZATION HERE*

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

    *INSERT VISUALIZATION HERE*

...



### Project 2: Real-time Tweet Sentiment Analysis 

- **Description**: A brief description of the project.
- **GitHub Repository**: [Link to GitHub Repo](https://github.com/conorbrooke77/Data-Science-ML-Project)
- **Live Demo**: [Link to Live Demo](https://www.youtube.com/)
- **Technologies Used**: Examples: Python, Scikit-Learn, Pandas, Matplotlib, StatsBomb.
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
  <img src="https://raw.githubusercontent.com/Arnab-Rajkhowa/Twitter-Sentiment-Analysis/master/tweet-dashboard.PNG" alt="Visualization1" width="380" height="200">
  <img src="https://miro.medium.com/v2/resize:fit:1400/1*AK0caqDJhnjt_PIihy5Ebw.png" alt="Visualization2" width="380" height="200">
  
- **Ethical Considerations**: 
  Describe any ethical concerns you had while working on the project data. Consider aspects like bias, fairness, or implications of predictive outcomes.

- **Regulations and Compliance**:
  - **GDPR Compliance**: Discuss how you ensured that the data handling and processing complied with GDPR regulations.

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

