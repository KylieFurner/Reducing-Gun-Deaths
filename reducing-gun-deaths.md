---
title: "Reducing Gun Deaths"
author: "Kylie"
output:
  html_document:  
    keep_md: true
    toc: true
    toc_float: true
    code_folding: hide
    fig_height: 6
    fig_width: 12
    fig_align: 'center'
---

## Background

The world is a dangerous place. In recent years there has been a lot of discussion about police shootings. Referencing FiveThirtyEight.com's report on [gun deaths in 2016](https://fivethirtyeight.com/features/gun-deaths/), I have created several visualizations to address some questions. I used a clean version of their data posted to their GitHub repo called [full_data.csv](https://github.com/fivethirtyeight/guns-data).

FiveThirtyEight’s visualizations focused on yearly averages. I decided to focus on a broader scope, and challenge myself to summarize and visualize seasonal trends across other variables in these data.

## Setup
```r
# Import datasets
data <- read.csv('https://raw.githubusercontent.com/fivethirtyeight/guns-data/master/full_data.csv')
```

## Data Wrangling


```r
# Clean and Wrangle the Data
yespolice <- data %>%
filter(police == 1)

nopolice <- data %>%
filter(police == 0)
```

## Intent and time of year
This chart tries to find a connection between intent and time of year. I was wondering if suicides might increase during the winter months due to seasonal depression. Or if deaths in general increased or decreased during a time of the year. However, there seems to be no correlations or patterns that I can see


```r
# Plot and Visualize
ggplot(data = data, aes(x=month)) + 
  geom_bar(aes(fill=intent)) + 
  facet_wrap(~year) + 
  theme_dark() + 
  scale_fill_brewer(palette = "OrRd")
```

![](chart1-1.png)<!-- -->

## Race and Police Involvment

This chart shows the deaths caused by police officers grouped by race. In the first chart we can clearly see that the most commonly killed race shot by police officers is white. 

```r
# Plot and Visualize
ggplot(data = yespolice, aes(x="")) + 
  geom_bar(aes(fill = race)) + 
  coord_polar("y", start=0) +
  theme_void() +
  labs(title = "Deaths With Police Involved") +
  scale_fill_brewer(palette = "Spectral")
```

![](chart2-1.png)<!-- -->


However, when we compare the chart to deaths without police involvement we see that the white and Hispanic categories change quite a lot. Police deaths decrease the proportion of white deaths but increase the proportion of Hispanic deaths by a notable amount. Examining both charts carefully you can actually see that all race deaths EXCEPT for white are increased when police are involved even if not by much.

```r
ggplot(data = nopolice, aes(x="")) + 
  geom_bar(aes(fill = race)) + 
  coord_polar("y", start=0) +
  theme_void() +
  labs(title = "Deaths Without Police Involved") +
  scale_fill_brewer(palette = "Spectral")
```

![](chart3-1.png)<!-- -->
