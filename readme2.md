**Most popular time of the year - Member vs. Casual** <br>
Arrange the days of the week in order for better visualization.
```
all_trips_v2$day_of_week <- ordered(
    all_trips_v2$day_of_week,
    levels = c(
        "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"
    )
)
```

Create a data frame to show number of trips by date.
```
heat_map_data <- all_trips_v2 %>%
    select(
        date,
        day_of_week,
        week,
        year
    ) %>%
    group_by(
        date
    ) %>%
    mutate(
        n_trips = n()
    ) %>%
    distinct(
        date,
        .keep_all = TRUE
    )
```

Create a heat map to show the most popular day.
```
p2 <- ggplot(
    heat_map_data,
    aes(
        x = as.numeric(week),
        y = day_of_week,
        fill = n_trips
    )
) +

# Use the viridis color to show the popularity of each day.
scale_fill_viridis(
    option = "D",
    direction = 1,
    name = "Number of trips"
) +

# Use a tile shape heat map.
geom_tile(
    color = "white",
    na.rm = FALSE
) +

# Separate the heat maps by year.
facet_wrap(
    "year",
    ncol = 1
) +

# Reverse the y-axis label. The days of the week is now reading from Monday to Sunday.
scale_y_discrete(
    limits = rev
) +

# Create x-axis labels to show the months of the year.
scale_x_continuous(
    expand = c(0,0),
    breaks = seq(1, 52, length = 12),
    labels = c("Jan", "Feb", "Mar", "Apr", "May", "Jun",
                "Jul", "Aug", "Sep", "Oct", "Nov", "Dec")
) + 

# 
theme_light() +

# Remove unnecessary labels
theme(
    axis.title = element_blank()
)
```

View the map.
```
p2
```

Create a data frame to show the number of trips by date and the rider's type.
```
heat_map_data_member_casual <- all_trips_v2 %>%
    select(
        date,
        day_of_week,
        week,
        year,
        member_casual,
    ) %>%

    group_by(
        member_casual,
        date
    ) %>%

    mutate(
        n_trips = n()
    ) %>%

    distinct(
        date,
        member_casual,
        .keep_all = TRUE
    )
```

Create a data frame for member riders.
```
member_heat_map <- heat_map_data_member_casual %>%
    filter(member_casual == "member")
```

Create a data frame for casual riders.
```
casual_heat_map <- heat_map_data_member_casual %>%
    filter(member_casual == "casual")
```

Create a heat map for member riders.
```
p2a_member <- ggplot(
    member_heat_map,
    aes(
        x = as.numeric(week),
        y = day_of_week,
        fill = n_trips
    )
) +
scale_fill_viridis(
    option = "D",
    direction = 1,
    name = "Number of trips"
) +
geom_tile(
    color = "white",
    na.rm = FALSE
) +
facet_wrap(
    "year",
    ncol = 1
) +
scale_y_discrete(
    limits = rev
) +
scale_x_continuous(
    expand = c(0,0),
    breaks = seq(1, 52, length = 12),
    labels = c("Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec")
) +
theme_light() +
theme(
    axis.title = element_blank()
) +
labs(title = "Member Riders")
```

Create a heat map for casual riders.
```
p2a_casual <- ggplot(
    casual_heat_map,
    aes(
        x = as.numeric(week),
        y = day_of_week,
        fill = n_trips
    )
) +
scale_fill_viridis(
    option = "D",
    direction = 1,
    name = "Number of trips"
) +
geom_tile(
    color = "white",
    na.rm = FALSE
) +
facet_wrap(
    "year",
    ncol = 1
) +
scale_y_discrete(
    limits = rev
) +
scale_x_continuous(
    expand = c(0,0),
    breaks = seq(1, 52, length = 12),
    labels = c("Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec")
) +
theme_light() +
theme(
    axis.title = element_blank()
) +
labs(title = "Casual Riders")
```

Combine the member riders and casual riders heat maps.
```
p2a <- ggarrange(
    p2a_member,
    p2a_casual,
    ncol = 1,
    nrow = 2,
    common.legend = TRUE,
    legend = "right"
)
```

View heat map.
```
p2a
```

## Note