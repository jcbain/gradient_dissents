---
title: "Geographic Distance Subsets in R"
date: 2018-02-18T17:33:28-06:00
draft: true
---

This was one of those moments where my Googling ability failed me. For learning purposes, this is great, but in terms of time, well I'm never getting those couple of days in February back. So this is a story about how I thought I solved a problem that had yet to be solved. This is also a story about how I was stupid to think that I was the first to solve a problem that must be fairly common. 

I'm interested in cities and their people and city metropolitan areas often span multiple counties, however, not all counties are equal particularly in terms of area. Seriously, look up San Bernardino county, California and see how many New England states you can fit inside it. Well, the problem is that you are often not interested in all of the super-geographies during an analysis. Instead, you are interested in some sub-geographies that make up a certain radius around a coordinate. This was my issue and this post is going to walk you through two different solutions.