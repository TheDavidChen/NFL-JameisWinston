JameisWinston
================
David Chen
12/29/2019

``` r
# Clean up R environment
rm(list = ls())

# Load in packages
library(tidyverse)
library(lubridate)
library(gghighlight)
```

    ## Warning: package 'gghighlight' was built under R version 3.6.2

``` r
# Read in the data
QBData <- readRDS('../../Data/AllYearsQBData.rds')
```

``` r
# Isolate Jameis' 2019 season
Jameis <-
  QBData %>%
  filter(Player == 'Jameis Winston' & Year == 2019)
```

Plot TD vs Ints

``` r
ggplot(QBData, aes(x = TD, y = Int)) +
  geom_point(alpha = 0.2) +
  labs(title = "Passing TDs vs Interceptions by Quarterbacks from 1970-2019",
             subtitle = 'Top rated QB for every team for each year (e.g. Dree Brees instead of Teddy Bridgewater)', 
       caption = 'Regular Season only | Data from: nfl.com/stats',
       y = 'Interceptions',
       x = 'Passing Touchdowns') +
  theme_minimal() +
  geom_point(data = Jameis, aes(x = TD, y = Int), color = 'red', size = 2) +
  geom_text(data = Jameis, aes(label=Player),hjust=-0.1,vjust=-0.5) 
```

![](JameisWinston_files/figure-gfm/Jameis%20Winston%20TDs/Ints-1.png)<!-- -->

``` r
# Save the images separately
ggsave('../../TD_Ints.png')
```

    ## Saving 7 x 5 in image

Who were the other top Int/TD players?

``` r
# Highlight the other unique players
gghighlight_point(QBData, aes(x = TD, y = Int), 
                  predicate = c(TD >= 50 | Int >= 30), label = Player) +
  labs(title = "TDs vs Interceptions by Quarterbacks from 1970-2019",
             subtitle = 'Top rated QB for every team for each year (e.g. Dree Brees instead of Teddy Bridgewater)', 
       caption = 'Regular Season Only | Data from: nfl.com/stats',
       y = 'Interceptions',
       x = 'Passing Touchdowns') +
  theme_minimal()
```

![](JameisWinston_files/figure-gfm/Other%20QBs%20TDs/Ints-1.png)<!-- -->

Plotting passing yards vs interceptions.

``` r
ggplot(QBData, aes(x = Yds, y = Int)) +
  geom_point(alpha = 0.3) +
  labs(title = "Passing Yards vs Interceptions by Quarterbacks from 1970-2019",
             subtitle = 'Top rated QB for every team for each year (e.g. Dree Brees instead of Teddy Bridgewater)', 
       caption = 'Regular Season Only | Data from: nfl.com/stats',
       y = 'Interceptions',
       x = 'Passing Yards') +
  theme_minimal() +
  geom_point(data = Jameis, aes(x = Yds, y = Int), color = 'red', size = 2) +
  geom_text(data = Jameis, aes(label=Player),hjust=0.46,vjust=-1.05) 
```

![](JameisWinston_files/figure-gfm/Jameis%20Passing/Ints-1.png)<!-- -->

``` r
# Save the images separately
ggsave('../../Yds_Ints.png')
```

    ## Saving 7 x 5 in image

Who were the other unique players?

``` r
gghighlight_point(QBData, aes(x = Yds, y = Int), 
                  predicate = c(Yds >= 5400 | Int >= 30), label = Player) +
  labs(title = "Passing Yards vs Interceptions by Quarterbacks from 1970-2019",
             subtitle = 'Top rated QB for every team for each year (e.g. Dree Brees instead of Teddy Bridgewater)', 
       caption = 'Regular Season Only | Data from: nfl.com/stats',
       y = 'Interceptions',
       x = 'Passing Yards') +
  theme_minimal() 
```

![](JameisWinston_files/figure-gfm/Other%20unique%20QBs%20Passing/Ints-1.png)<!-- -->
