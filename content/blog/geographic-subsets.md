---
title: "Geographic Distance Subsets in R"
date: 2018-02-18T17:33:28-06:00
draft: true
---

This was one of those moments where my Googling ability failed me. For learning purposes, this is great, but in terms of time, well I'm never getting those couple of days in February back. So this is a story about how I thought I solved a problem that had yet to be solved. This is also a story about how I was stupid to think that I was the first to solve a problem that must be fairly common. 

I'm interested in cities and their people and city metropolitan areas often span multiple counties, however, not all counties are equal particularly in terms of area. Seriously, look up San Bernardino county, California and see how many New England states you can fit inside it. Well, the problem is that you are often not interested in all of the super-geographies during an analysis. Instead, you are interested in some sub-geographies that make up a certain radius around a coordinate. This was my issue and this post is going to walk you through two different solutions: one out of naïveté and the other a bit more researched.

Kansas City is the perfect candidate to test subsetting around a coordinate. It's metropolitan area spans 9 counties and 2 states (the majority in Missouri and some in Kansas). Just to be exhaustive, I will be collecting on a 15 county area. It also happens to be my place of birth and where I spent the majority of the first 18 years of my life. I will be using `tidycensus` to gather the Census tracts for each of these counties along with the 2015 American Community Survey estimates on the proportion of African Americans living in each tract. Take a look at my [previous post](https://jcbain.github.io/blog/diversity-with-tidycensus/) for a more detailed explanation of using `tidycensus` to collect ACS data. First we will load in our packages and then collect our data.

```r
library(tidyverse)  
library(tidycensus)
library(sf) 
library(vegan)
library(viridis)
library(tigris)
library(ggthemes)

options(tigris_class = "sf")
options(tigris_use_cache = TRUE)

# ACS 2015 race variable codes

racevars = c('B02001_001E', 'B02001_003E')

# Counties 

places <- c('MO,Clay', 'MO,Jackson', 'MO,Platte', 'MO,Cass', 'MO,Lafayette',
            'MO,Ray', 'MO,Clinton', 'MO,Bates', 'MO,Caldwell', 'KS,Johnson',
            'KS,Wyandotte', 'KS,Leavenworth', 'KS,Miami', 'KS,Linn', 'KS,Franklin')

# Collect the variables

pop <- reduce(
  map(places, function(x) {
    get_acs(geography = "tract", variables = racevars, 
            state = str_split(x ,pattern = ',')[[1]][1],county = str_split(x,pattern = ',')[[1]][2])
  }), 
  rbind
)

# Collect the simple features for mapping

geographies <- reduce(
  map(places, function(x) {
    get_acs(geography = "tract",  variables = "B01003_001",
            state = str_split(x ,pattern = ',')[[1]][1],county = str_split(x,pattern = ',')[[1]][2] ,
            geometry = TRUE)
  }), 
  rbind
)
```

Then I have to do some pre-processing. `B02001_001E` is the variable for the total number of people estimate for the selected geography and `B02001_003E` is the estimate of African Americans within a geography. I want a proportion instead of raw count so I have to convert the current `pop` data frame into wide format. I then join this back to the geographic simple features data frame `geographies` so that we can visualize the proportion graphically.

```r
pop %<>%
  select(-moe) %>%
  spread(variable, estimate) %>%
  group_by(GEOID) %>%
  mutate(aa = (B02001_003/B02001_001)) %>%
  ungroup()

kc <- geographies %>%
  left_join(pop, by = 'GEOID') 
```

Let's go ahead and visuzlize what we have here.
