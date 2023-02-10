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

**Preview data** <br>
Preview the data to perform data consistancy check, such as data structure and column names. 
```
str(Dec_21)
str(Jan_22)
str(Feb_22)
str(Mar_22)
str(Apr_22)
str(May_22)
str(Jun_22)
str(Jul_22)
str(Aug_22)
str(Sep_22)
str(Oct_22)
str(Nov_22)
```
Perform colume names check to ensure consistancy.
```
colnames(Dec_21)
colnames(Jan_22)
colnames(Feb_22)
colnames(Mar_22)
colnames(Apr_22)
colnames(May_22)
colnames(Jun_22)
colnames(Jul_22)
colnames(Aug_22)
colnames(Sep_22)
colnames(Oct_22)
colnames(Nov_22)
```

**Combine datasets** <br>
Combine all 12 datasets into a single data frame.
```
all_trips <- bind_rows(
    Dec_21, Jan_22, Feb_22, Mar_22, Apr_22, May_22, 
    Jun_22, Jul_22, Aug_22, Sep_22, Oct_22, Nov_22
)
```

**Prepare dataset** <br>
Use $ operator to extract the started_at and ended_at columns from the data frame. Then, we convert started_at and ended_at data type from "char" to "POSIXct" type to help with time manipulation. Dates store in the POSIX format are more accurate compare to the built-in as.Date function. After the conversion is completed, arrange the started_at column in ascending order to make it easier to analyze.
```
all_trips$started_at <- as.POSIXct(
    all_trips$started_at,
    format = "%Y-%m-%d %H:%M:%S"
)

all_trips$ended_at <- as.POSIXct(
    all_trips$ended_at,
    format = "%Y-%m-%d %H:%M:%S"
)

all_trips <- all_trips %>%
    arrange(started_at)
```

**Calculate ride length** <br>
Calculate the length of each ride to get a better sense of the data layout. Convert ride_length to numeric for calculation.
```
# Add and calculate the ride_length column
all_trips$ride_length <- difftime(
    all_trips$ended_at,
    all_trips$started_at,
    units = "secs"
)

# Convert ride_length to numeric
all_trips$ride_length <- as.numeric(
    as.character(all_trips$ride_length)
)
```

**Create columns for date, month, day, and year** <br>
Separate each date part for later visualization that plots by date, year, month, and day.
```
#Add year column
all_trips$year <- format(
    all_trips$started_at,
    "%Y"
)

#Add month column
all_trips$month <- format(
    all_trips$started_at,
    "%m"
)

#Add week column
all_trips$week <- format(
    all_trips$started_at,
    "%W"
)

#Add day column
all_trips$day <- format(
    all_trips$started_at,
    "%d"
)

#Add day of week column
all_trips$day_of_week <- format(
    all_trips$started_at,
    "%A"
)

#Add date column
all_trips$date <- format(
    all_trips$started_at,
    "%Y:%m:%d"
)

#Add time column
all_trips$time <- format(
    all_trips$started_at,
    "%H:%M:%S"
)
```

**Inspect dataset** <br>
Inspect the dataset to see if any unexpected items that were out of normal scope. 
```
arrange(all_trips, ride_length)
```

Inspect the dataset to see if any duplicated ride ID because the ride_id column should be unique on each ride. 
```
sum(duplicated(all_trips$ride_id)
```

**Remove ride length rows with negative values** <br>
After inspecting the dataset, notice there were a few instances where the ride lengths had negative values. Rows with ride length less than zero should be removed.
```
#Filter data by ride_length
all_trips_v2 <- all_trips %>%
    filter(!ride_length < 0)
```

**Remove rows without station name** <br>
In addition, some station names and station IDs were missing. These data should also be removed from the dataset.
```
#Filter data by start_station_name and end_station_name
all_trips_v2 <- all_trips_v2 %>%
    filter(
        !(is.na(start_station_name) | start_station_name == "")
    ) %>%
    filter(
        !(is.na(end_station_name) | end_station_name == "")
    )
```

**Get ride length summary** <br>
Summarize the ride length to get a better sense of the data layout.
```
summary(all_trips_v2$ride_length)
```

**Save file** <br>
Save a .csv file copy for future data exploration.
```
fwrite(
    all_trips_v2,
    "./Downloads/Cyclistic Case Study/all_trips_v2.csv",
    col.names = TRUE,
    row.names = FALSE
)
```

## Data Visualization Process
**Install and load visualization tools** <br>
```
install.packages("leaflet")
install.packages("viridis")
install.packages("ggpubr")
library(leaflet)
library(viridis)
library(ggpubr)
```

**Create map dataset** <br>
To better organize the data, a map data frame is created to see which station was the most popular.
```
map_data <- all_trips_v2 %>%
    select(
        start_station_name,
        start_lat,
        start_lng
    ) %>%
    group_by(
        start_station_name
    ) %>%
    mutate(
        n_trips = n()
    ) %>%
    distinct(
        start_station_name,
        .keep_all = TRUE
    )
```

Get a summary to check the range of n_trips. 
```
summary(map_data$n_trips)
```

From the n_trips summary, the range was between 0 to 71956. Set up a sequence of value that will be shown on the legend to indicate number of trips.
```
bin_range <- seq(0, 80000, by = 10000)
```

Set up a color palette. Call the colorBin function from leaflet to create a new palette function.
```
mypalette <- colorBin(
    palette = "viridis",
    domain = map_data$n_trips,
    na.color = "transparent",
    bins = bin_range
)
```

Create map text labels.
```
text_label <- paste(
    "Station name: ", map_data$start_station_name, "<br/>",
    "Number of trips: ", map_data$n_trips, sep = ""
) %>%
lapply(htmltools::HTML)
```

Create leaflet.
```
p1 <- leaflet(map_data) %>%
    addTiles() %>%

    # Use setView method to manipulate the map widget
    setView(
        lng = -87.6051, lat = 41.8919, zoom = 11.5
    ) %>%
    addProviderTiles("Esri.WorldGrayCanvas") %>%

    # Add circle markers to the map
    addCircleMarkers(
        ~start_lng, ~start_lat,
        fillColor = ~mypalette(n_trips),
        fillOpacity = 0.7,
        color = "white",
        radius = 8,
        stroke = FALSE,
        label = mytext,
        labelOptions = labelOptions(
            style = list(
                "font-weight" = "normal,
                padding = "2px 8px"
            ),
        textsize = "12px",
        direction = "auto"
        )
    ) %>%

    # Add a legend to the map.
    addLegend(
        pal = mypalette,
        values = ~n_trips,
        opacity = 0.8,
        title = "Number of trips",
        position = "bottomright"
    )
```

View the map.
```
p1
```



## References
* UC Berkeley Department of Statistics (https://www.stat.berkeley.edu/~s133/dates.html)
* rdrr.io (https://rdrr.io/cran/leaflet/man/colorNumeric.html)
* Leaflet (https://rstudio.github.io/leaflet/colors.html)
* Package Leaflet (https://cran.r-project.org/web/packages/leaflet/leaflet.pdf)


