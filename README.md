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
First install package and load package by running library
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
book_df <- read_csv("hotel_bookings.csv"
```
#### Explore Data 
In the Data Exploration step, we will conduct a general examination of the dataset. This includes checking the number of rows and columns, inspecting data types, identifying missing values in the data, and examining sample data within the table.

```{r}
# view head of data frame
head(book_df)
# view structure of data frame as number of columns and rows, 
# column name, data type and example of data 
str(book_df)
glimpse(book_df) 
# view only column name 
colnames(book_df)
# show summary of data 
summary(book_df)
# show summary of NA in each column
summary(is.na(book_df)) # column children have 4 NA
# show only rows have NA
subset(book_df, is.na(children))
```
#### Data Cleaning
- Begin by deleting rows with missing values.
- Next, rename the 'ard' column to 'average_daily_rate' for better clarity.
- Change the data type of the 'arrival_date_month' column from Char to int.
- Combine the values of 'arrival_date_year,' 'arrival_date_month,' and 'arrival_date_day_of_month' into 'arrival_date' and format it as YYYY-MM-DD.

```{r}
# Data Cleaning
book_df_clean <- book_df %>%
  na.omit() %>% # Note Delete rows have missing value
  rename(average_daily_rate = adr) %>% # Note Change column name adr to Average Daily Rate
  mutate(
    arrival_date_month = as.integer(factor(arrival_date_month, levels = month.name)),
    arrival_date = paste(arrival_date_year, sprintf("%02d", arrival_date_month), 
                         sprintf("%02d", arrival_date_day_of_month), sep = "-"))
# Note change data type in column arrival_date_month from char to int 
    # Note combine date of arrival_date_year, arrival_date_month and arrival_date_day_of_month

#View(book_df_clean)

#glimpse(book_df_clean)
```

- Combine the number of guests from the 'adults,' 'children,' and 'babies' columns into a new column named 'number_of_guests.'
- Sum the number of nights spent on weekends ('stays_in_weekend_nights') and weekdays ('stays_in_week_nights') to create a new column called 'day_of_stays' representing the total length of stay.
- Select columns to exclude from the dataset.

```{r}
# sum number of adults, children and babies and create new column 
# sum number of stays_in_week_nights and stays_in_weekend_nights in new column day_of_stays
book_df_clean2 <- book_df_clean %>% 
  mutate(number_of_guests = adults + children + babies ) %>%
  mutate(day_of_stays = stays_in_weekend_nights + stays_in_week_nights) %>% 
  select(-arrival_date_day_of_month, -arrival_date_month, -arrival_date_year,
         -arrival_date_week_number, -adults, -children, -babies, 
         -stays_in_weekend_nights, -stays_in_week_nights)
 
#View(book_df_clean2)
```
After completing the Data cleaning process, save the file in CSV format using the command.

```{r}
# save file csv
write.csv(book_df_clean2, file = "hotel_bookings_clean")
```
