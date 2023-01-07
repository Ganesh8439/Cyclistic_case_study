# Cyclistic_case_study
---
title: "Cyclistic Case Study"
author: "Ganesh I"
date: "2023-01-07"
output: html_document
---

## Loading all data sets

```{r eval=FALSE, include=FALSE}
setwd("C:/Users/91880/Downloads/Cylistic_2022_data_v1/2022_csv")
library(tidyverse)
jan_2022 <- read_csv("202201-divvy-tripdata.csv")
feb_2022 <- read_csv("202202-divvy-tripdata.csv")
mar_2022 <- read_csv("202203-divvy-tripdata.csv")
apr_2022 <- read_csv("202204-divvy-tripdata.csv")
may_2022 <- read_csv("202205-divvy-tripdata.csv")
jun_2022 <- read_csv("202206-divvy-tripdata.csv")
jul_2022 <- read_csv("202207-divvy-tripdata.csv")
aug_2022 <- read_csv("202208-divvy-tripdata.csv")
sep_2022 <- read_csv("202209-divvy-publictripdata.csv")
oct_2022 <- read_csv("202210-divvy-tripdata.csv")
nov_2022 <- read_csv("202211-divvy-tripdata.csv")
dec_2022 <- read_csv("202212-divvy-tripdata.csv")
```

## Merging into one dataframe

```{r eval=FALSE, include=FALSE}
rides_2022 <- bind_rows(jan_2022,feb_2022,mar_2022,apr_2022,may_2022,jun_2022,
                        jul_2022,aug_2022,sep_2022,oct_2022,nov_2022,dec_2022)
glimpse(rides_2022)
```

## Removing unwanted columns

```{r eval=FALSE, include=FALSE}
rides_2022 <- select(rides_2022,-c(start_lat, start_lng, end_lat, end_lng))
```

## Getting to know the data

```{r eval=FALSE, include=FALSE}
summary(rides_2022)
unique(rides_2022$member_casual)
unique(rides_2022$rideable_type)
table(rides_2022$member_casual)
```

## Creating a new column for ride length, date, month and day of week

```{r eval=FALSE, include=FALSE}
rides_2022$ride_length <- difftime(rides_2022$ended_at,rides_2022$started_at)
rides_2022$date <- as.Date(rides_2022$started_at)
rides_2022$month <- format(as.Date(rides_2022$date), "%m")
rides_2022$day_of_week <- format(as.Date(rides_2022$date), "%A")
```

## Converting ride length into numeric and deleting NA rows

```{r eval=FALSE, include=FALSE}
rides_2022$ride_length <- as.numeric(as.character(rides_2022$ride_length))
rides_2022 <- rides_2022 %>% drop_na()
```
