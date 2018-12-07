+++
draft = true
image = "img/post7/denver_postcard.jpg"
showonlyimage = false
date = "2018-12-01T20:11:33-05:00"
title = "The Opportunity of Geography Part 1: How Denver Highways Segregate Communities"
weight = 11
+++

Sunday nights are for laundry, mental preparation for the week ahead and House Hunters. It's a bit of a mental reprieve for me; for a few minutes out of the week I can forget about my life and focus on the lives of complete strangers who are making one of the biggest financial decisions they'll ever step into. Sure, I know they choose their house before filming (logistically, that's the only way this show could work) but I still find it refreshing to watch seemingly boring people discuss what sort of floor plan will work for their dinner parties they hope to have. People also like to make their home lives convenient for their work lives and the most apparent indication of this the trade-off discussions between a dream home and proximity to work. Sometimes this results in smaller square footage in order to be within throwing distance of the office. Other times its the manicured McMansion in exchange for a part time job driving to work every week. 

Whether we realize it or not, transportation plays a key role in our lives and transportation is made possible by the appropriate infrastructure. Tramlines, bike paths, highways, they can all bring about opportunity for communities. But opportunity for whom and what expense? This post is the first in a series of posts that will explore how transportation shapes the lives of communities. 

The story begins in Denver, Colorado. More specifically, the highway system in Denver and how it creates borders between opportunity. Borders are often arbitrary and invisible (think countries). These types of borders create their own types of problems but this isn't that sort of story. Instead, the highways of Denver (and many [other cities in the US](https://www.theatlantic.com/business/archive/2016/03/role-of-highways-in-american-poverty/474282/)) establish physical borders that separate communities. But before we get into any of that, let's first set the scene. 

For those of you unfamiliar with Denver, the population in 2010 was a bit north of 600,000. Since then, the population has grown nearly 17% in the past 7 years making it one of the fastest growing cities in all of the United States. The city supports a metropolitan population of 2.9 million people all of whom enjoy an average of 300 days of sunshine a year. Throw in the Rockies as your backdrop and Denver is one the most appealing cities for people who straddle the fence between outdoors enthusiast and city-slickin'. 

Denver also resides at the confluence of I-70, a major East-West artery of the continental United states, and I-25, which runs North-South. Highways are noisy, dangerous and dirty, but they are also a necessity for many people's lives. Getting to and from work, family and fun would be hardly worth it without the ease of cruising 70+ miles down the interstate. This, like many things in life, poses a classic trade-off scenario. On one hand, residing next to the highway means listening to semis fly by your house every second of every day; on the other, getting to where you need to go is faster, which translates to more time with the family (whomever that may be 🐶). So the first question that I wanted to look at was "Is living by the highway more or less desirable?" To answer this question, I made my way to [Denver's Open Data portal](https://www.denvergov.org/opendata). Desirability is a complex indicator to measure but what is reasonable is to assess the neighborhood economic situations of a city. I'm going to make a gross generalization/assumption here, but living in poorer conditions is less desirable than living in more economically fortunate ones. I found a [data-set of the Housing and Urban Development's assessment of poverty in middle income for each Census tract for 2014 in the city of Denver](https://www.denvergov.org/opendata/dataset/city-and-county-of-denver-hud-income-levels)<sup>1</sup>. This provided me with a decent set of economic data to answer this question. I also needed [highway data](https://stackoverflow.com/questions/25579868/how-to-add-footnotes-to-github-flavoured-markdown)<sup>2,3</sub> in order to evaluate the geographic component of this question. 

I thought to first look at [Census tracts](https://www.denvergov.org/opendata/dataset/city-and-county-of-denver-census-neighborhood-demographics-2010)<sup>4</sup> that touch highways and then those tracts that touch tracts that touch highways in case there was any gradient like behavior in poverty levels as people got further away from highways.

![Ethnicity Gif](/img/post7/hwy_touches_map.png)
<sub>*Map 1*: This map highlights those Census tracts that touch a highway along with those tracts that touch tracts that touch a highway.</sub>

This direction ended in some simple exploration. There was no reason to believe that the distribution of low-income individual proportions were any different for those who live in areas touching highways as opposed to those living a bit farther out.

![Boxplot](/img/post7/box_plot.png)
<sub>*Fig 1*: The distribution of poverty isn't much different between those blocks that touch highways and those that don't. In these particular data, the mean poverty proportion is higher for those that touch the highway but not enough to warrant difference.</sub>

But this is certainly not where the story ends. In fact, by the time we get to the end of this post, the story will just be beginning. This is where we start to look at what highways indicate in terms of communities. Perhaps highways aren't repellents but instead fences. Let's take a step in a different direction and start looking at race and ethnicity proportions in each neighborhood of the city.


![Ethnicity Gif](/img/post7/hwy_plot.gif)
<sub>*Map 2*: The proportion of each race/ethnicty for each neighborhood in Denver.</sub>

This is beginning to paint a picture. The first noticeable observation from the gif above is that the city is rather segregated in some places. But how does this translate to highways and poverty? I thought to [partition the data](https://papers.nips.cc/paper/5605-partition-wise-linear-models.pdf) into neighborhoods by dominate ethnicity in that neighborhood. Zooming out, Denver has a lot neighborhoods of primarily white or primarily hispanic individuals. This isn't to say that other races and ethnicities don't live in the Mile High city, they just don't happen to be the most prevalent in any of Denver's neighborhoods (save for two where the majority is black individuals). The reason for this is a whole other post or five. 

I began to start looking into the relationship between the ethnicity/race and poverty in the Denver neighborhoods first. Does the ethnic/racial makeup of a neighborhood translate to differing levels of opportunity? Since the data were partitioned along the most prevalent demographic group, the proportion of the dominant population was compared against the proportion of the population that were low income in the neighborhood. Using bayesian linear regression, the relationship between poverty and ethnicity proportion were modelled for both neighborhoods were predominantly white or hispanic.

![Scatter Plot](/img/post7/scatter.png)
<sub>*Fig 2*: This scatter plot demonstrates that white individuals disproportionally live in better economic conditions than hispanic individuals. The greater the proportion of white people, the smaller the proportion of low income individuals there are. However, hispanic individuals demonstrate the exact opposite in which the higher proportion of hispanic individuals translates to higher levels of poverty.</sub>

The models were created using the [`brms` package](https://cran.r-project.org/web/packages/brms/index.html) in `R` and while bayesian analysis doesn't provide a single point estimate of the linear trend for each population's relationship with poverty, it does provide a posterior probability distribution for the slope parameter. In both models, the trend is clear, as the proportion of hispanic population increases so does poverty while the opposite is true for the predominantly white neighborhoods. As the the proportion of the white population increases then the proportion of poverty in that neighborhood decreases. 

![Distribution Plot](/img/post7/posteriors.png)
<sub>*Fig 3*: This plot shows the posterior slope probability distributions for the relationship between ethnicity and poverty. Using a bayesian linear model approach, the 95% credible interval visually demonstrates that these distributions will probably not overlap, which indicates different behaviors in the trend.</sub>

But how are these populations distributed across the city? Enter the highways again. Unsurprisingly, these ethnic/racial predominant neighborhoods are contiguous creating larger areas of either predominantly white or predominantly hispanic populations. What divides these populations? Highways. I-25 seems to not just divide the city into east and west but also into enclaves of hispanic and white individuals. The same is true for I-70 in the northern part of the city. 

![Ethnicity Map](/img/post7/neigh_ethn_map.png)
<sub>*Map 3*: This map displays the most prevalent ethnicity per neighborhood in Denver with the shade of color indicate the proportion of the population. When looking at the map, populations are separated by highways and are kept relatively contiguous based on these physical borders.</sub>

Remember, neighborhoods also tend to get poorer as the proportion of the hispanic population increases while the opposite is true for the white population. This means that highways are literally separating opportunity. Now, teasing apart economic variables with demographic ones is very difficult. The United States has a dark and complicated history with holding back minority populations. These are issues that I will begin to tackle in future posts of opportunity and geography.

This first post doesn't dive into the details about the methods used to carry out this analysis. If you are wanting to take a look at the script I used, take a look [here](https://github.com/jcbain/fun_side_projects/tree/master/denver_opportunity).

#### Footnotes
1. [HUD Income Levels](https://www.denvergov.org/opendata/dataset/city-and-county-of-denver-hud-income-levels) by *the Office of Economic Development*
2. [TIGER/Line Shapefile, 2012, county, Denver County, CO, All Roads County-based Shapefile](https://stackoverflow.com/questions/25579868/how-to-add-footnotes-to-github-flavoured-markdown) by *U.S. Department of Commerce, U.S. Census Bureau, Geography Division & Geographic Products Branch*
3. [Route Type Codes and Definitions](https://www.census.gov/geo/reference/rttyp.html) by *the US Census*
4. [Census Neighborhood Demographics (2010)](https://www.denvergov.org/opendata/dataset/city-and-county-of-denver-census-neighborhood-demographics-2010) by *City and County of Denver, Technology Services / GIS Data *