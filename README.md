# Data_Analysis_Project_data_Cleaning_withR

### Project Overview
Data cleaning is an essential step in data analysis, involving the identification and correction of errors to enhance data quality.In this project, we will utilize R programming for data cleaning, working with the 'Hotel booking demand' public dataset from Kaggle. Upon completing the data cleaning process, we will obtain a dataset ready for use in subsequent steps.

### Tool
  - R-Studio

### The Data Cleaning steps for this project include:
1. Installing packages in R-Studio.
2. Importing and inspecting the dataset.
3. Performing Data Cleaning processes such as:
	- Renaming certain columns for better clarity.
	- Deleting rows with missing data.
	- Combining values from multiple columns.
	- Changing the date format in the dataset.
	- Separating unwanted columns from the dataset.

### Data cleaning with R-programming
```{r}
# Project Data Cleaning with R

# install packages  and load library
install.packages("tidyverse")
install.packages("skimr")
install.packages("janitor")
install.packages("dplyr")
install.packages("lubridate")

library(tidyverse)
library(skimr)
library(janitor)
library(dplyr)
library(lubridate)
```

```{r}
# import and review data
# Download dataset from https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand
book_df <- read_csv("hotel_bookings.csv")
# for view all data View(book_df)

# view head of data frame
head(book_df)
```
