# Cyclistic Case Study

## Summary

## Table of Contents
* [Final Report](#final-report)
* [Case Study Brief](#case-study-brief)
* [Data Cleaning Process](#data-cleaning-process)
* [Data Visualization Process](#data-visualization-process)


## Final Report


## Case Study Brief
**Scenario** <br>
You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.

**About the company** <br>
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. <br>

Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members. <br>

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the pricing flexibility helps Cyclistic attract more customers, Moreno believes that maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a very good chance to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs. <br>

Moreno, the director of marketing, has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. In order to do that, however, the marketing analyst team needs to better understand how annual members and casual riders differ, why casual riders would buy a membership, and how digital media could affect their marketing tactics. Moreno and her team are interested in analyzing the Cyclistic historical bike trip data to identify trends.


## Data Cleaning Process
**Description** <br>
For the purpose of this study, only data collected between December 2021 - November 2022 will be assessed. Please note that Cyclistic is a fictional company; the dataset has been made available by Motivate International Inc., which operates the City of Chicago's Divvy bicycle sharing service. The license to use this dataset can be found [here.](https://ride.divvybikes.com/data-license-agreement) <br>

**Install and load required packages** <br>
```
install.packages("tidyverse")
library(tidyverse)
```

**Upload raw datasets** <br>
```
Dec_21 <- read.csv("./Downloads/Cyclistic Case Study/202112-divvy-tripdata.csv")
Jan_22 <- read.csv("./Downloads/Cyclistic Case Study/202201-divvy-tripdata.csv")
Feb_22 <- read.csv("./Downloads/Cyclistic Case Study/202202-divvy-tripdata.csv")
Mar_22 <- read.csv("./Downloads/Cyclistic Case Study/202203-divvy-tripdata.csv")
Apr_22 <- read.csv("./Downloads/Cyclistic Case Study/202204-divvy-tripdata.csv")
May_22 <- read.csv("./Downloads/Cyclistic Case Study/202205-divvy-tripdata.csv")
Jun_22 <- read.csv("./Downloads/Cyclistic Case Study/202206-divvy-tripdata.csv")
Jul_22 <- read.csv("./Downloads/Cyclistic Case Study/202207-divvy-tripdata.csv")
Aug_22 <- read.csv("./Downloads/Cyclistic Case Study/202208-divvy-tripdata.csv")
Sep_22 <- read.csv("./Downloads/Cyclistic Case Study/202209-divvy-publictripdata.csv")
Oct_22 <- read.csv("./Downloads/Cyclistic Case Study/202210-divvy-tripdata.csv")
Nov_22 <- read.csv("./Downloads/Cyclistic Case Study/202211-divvy-tripdata.csv")
```

## Data Visualization Process





