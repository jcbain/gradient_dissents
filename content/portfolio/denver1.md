+++
draft = true
image = "img/post7/denver_postcard.jpg"
showonlyimage = false
date = "2018-12-01T20:11:33-05:00"
title = "The Opportunity of Geography (Part 1)"
weight = 11
+++

Sunday nights are for laundry, mental preparation for the week ahead and House Hunters. It's a bit of a mental reprieve for me; for a few minutes out of the week I can forget about my life and focus on the lives of complete strangers who are making one of the biggest financial decisions they'll ever step into. Sure, I know they choose their house before filming (logistically, that's the only way this show could work) but I still find it refreshing to watch seemingly boring people discuss what sort of floor plan will work for their dinner parties they hope to have. People also like to make their home lives convenient for their work lives and the most apparent indication of this the trade-off discussions between a dream home and proximity to work. Sometimes this results in smaller square footage in order to be within throwing distance of the office. Other times its the manicured McMansion in exchange for a part time job driving to work every week. 

Whether we realize it or not, transportation plays a key role in our lives and transportation is made possible by the appropriate infrastructure. Tramlines, bike paths, highways, they can all bring about opportunity for communities. But opportunity for whom and what expense? This post is the first in a series of posts that will explore how transportation shapes the lives of communities. 

The story begins in Denver, Colorado. More specifically, the highway system in Denver and how it creates borders between opportunity. Borders are often arbitrary and invisible (think countries). These types of borders create their own types of problems but this isn't that sort of story. Instead, the highways of Denver (and many [other cities in the US](https://www.theatlantic.com/business/archive/2016/03/role-of-highways-in-american-poverty/474282/)) establish physical borders that separate communities. But before we get into any of that, let's first set the scene. 

For those of you unfamiliar with Denver, the population in 2010 was a bit north of 600,000. Since then, the population has grown nearly 17% in the past 7 years making it one of the fastest growing cities in all of the United States. The city supports a metropolitan population of 2.9 million people all of who enjoy an average of 300 days of sunshine a year. Throw in the Rockies as your backdrop and Denver is one the most appealing cities for people who straddle the fence between outdoors enthusiasts and city-slickin'. 

Denver also resides at the confluence of I-70, the major East-West artery of the continental United states, and I-25, which runs North-South. Highways are noisy, dangerous and dirty, but they are also a necessity for many people's lives. Getting to and from work, family and fun would be hardly worth it without the ease of cruising 70+ miles down the interstate. This, like many things in life, poses a classic trade-off scenario. On one hand, residing next to the highway means listening to semis fly by your house every second of every day; on the other, getting to where you need to go is faster, which translates to more time with the family (whomever that may be 🐶). So the first question that I wanted to look at was "Is living by the highway more or less desirable?" To answer this question, I made my way to [Denver's Open Data portal](https://www.denvergov.org/opendata). Desirability is a complex indicator to measure but what is reasonable is to assess the neighborhood economic situations of a city. I'm going to make a gross generalization/assumption here, but living in poorer conditions is less desirable than living in more economically fortunate ones. I found a [data-set of the Housing and Urban Development's assessment of poverty in middle income for each Census tract for 2014 in the city of Denver](https://www.denvergov.org/opendata/dataset/city-and-county-of-denver-hud-income-levels). This provided me with a decent set economic data to answer this question. I also needed highway data in order to evaluate the geographic component of this question. 

I thought to first look at Census tracts that touch highways and then those tracts that touch tracts that touch highways in case there was any gradient like behavior in poverty levels as people got further away from highways.

![Ethnicity Gif](/img/post7/hwy_touches_map.png)
<sub>*Map 1*: This map highlights those Census tracts that touch a highway along with those tracts that touch tracts that touch a highway.</sub>

This direction ended in some simple exploration. There was no reason to believe that the distribution of low-income individual proportions were any different for those who live in areas touching highways as opposed to those living a bit farther out.

![Boxplot](/img/post7/box_plot.png)
<sub>*Fig 1*: The distribution of poverty isn't much different between those blocks that touch highways and those that don't. In these particular data, the mean poverty proportion is higher for those that touch the highway but not enough to warrant difference.</sub>

But this is certainly not where the story ends. In fact, by the time we get to the end of this post, the story will just be beginning. This is where we begin to look at what highways begin to indicate in terms of communities. Perhaps highways aren't repellents but instead fences. Let's take a step in a different direction and start looking at race and ethnicity proportions in each neighborhood of the city.


![Ethnicity Gif](/img/post7/hwy_plot.gif)
<sub>*Map 2*: The proportion of each race/ethnicty for each neighborhood in Denver.</sub>

This is beginning to paint a picture. The first noticeable observation from the gif above is that the city is rather segregated in some places. But how does this translate to highways and poverty? I thought to [partition the data](https://papers.nips.cc/paper/5605-partition-wise-linear-models.pdf) into neighborhoods by dominate ethnicity in that neighborhood. Zooming out, Denver has a lot neighborhoods of primarily white or primarily hispanic individuals. This isn't to say that other races and ethnicities don't live in the Mile High city, they just don't happen to be the most prevalent in any of Denver's neighborhoods (save for two where the majority is black individuals). The reason for this is a whole other post or five. 

![Scatter Plot](/img/post7/scatter.png)
<sub>*Fig 2*: This scatter plot demonstrates that white individuals disproportionally live in better economic conditions than hispanic individuals. The greater the proportion of white people, the smaller the proportion of low income individuals there are. However, hispanic individuals demonstrate the exact opposite in which the higher proportion of hispanic individuals translates to higher levels of poverty.</sub>

![Distribution Plot](/img/post7/posteriors.png)
<sub>*Fig 3*: This plot shows the posterior slope probability distributions for the relationship between ethnicity and poverty. Using a bayesian linear model approach, the 95% credible interval visually demonstrates that these distributions will probably not overlap, which indicates different behaviors in the trend.</sub>

![Ethnicity Map](/img/post7/neigh_ethn_map.png)
<sub>*Map 3*: This map displays the most prevalent ethnicity per neighborhood in Denver with the shade of color indicate the proportion of the population. When looking at the map, populations are separated by highways and are kept relatively contiguous based on these physical borders.</sub>