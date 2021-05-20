---
layout: post
title: Notes on technical analysis - Indicators
date: 2021-05-20 08:00:00:00 +0600
description: Quick guide for technical indicators# Add post description (optional)
img: 2020-04-12-docker.png # Add image post (optional)
fig-caption: Stock chart # Add figcaption (optional)
tags: [finance, stocks]
---

I've been learning about technical analysis and how is expected that some scenarios repeat

# VWAP

Volume Weighted Average Price (or VWAP) is a trading bechmark that will give you the average price a security has been traded through the day. This value also takes into account the volume and not only the price, therefore if an stock is traded more often at a certain price it will have more weight. For example:

| Price | Volume |
|-------|--------|
| 10    |  5     |
| 12    |  5     |
| 14    |  10    |

The formula is: ![vwap-formula]({{site.baseurl}}/assets/img/posts/2021-05-30-vwap-formula.png)

In this scenario the VWAP will be: ((10 * 5) + (12 * 5) + (14 * 10)) / 20 = 12.5

## When to use it
The theory here suggest that institutional owners will use the VWAP as reference for long or short trading, and the VWAP will act as a resistance because of the large buys or sells.

