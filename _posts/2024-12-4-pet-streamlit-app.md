---
layout: post
title:  "Making a Web App to Uncover Pet Adoptions"
date: 2024-12-04
author: Almendra Clawson
description: "Using our data gathered from the Petfinder API to make a Streamlit App"
---

<p class="intro"><span class="dropcap">A</span>re you interested in understanding pet adoption trends in your area? In this post, I’ll show you how I used the Petfinder API to analyze the availability of pets near me, specifically exploring which organizations have the highest proportion of cats available for adoption.</p>

### Exploring our Petfinder Data

From my previous post, I used the free [Petfinder API](https://www.petfinder.com/developers/) to gather data to analyze the cats that were available to adopt in Utah. Now that I have dataset curated with information on the pet available to adopt in Utah, I wanted to answer this question: How does compare the distribution of the dogs available for adoption compared to cats?

### Using Streamlit to Create a Web App

For those that aren't familiar with programming, it can be difficult to modify data in order to answer questions or recieve insights. 