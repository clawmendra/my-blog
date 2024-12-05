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

For those that aren't familiar with programming or data science, it can be difficult to modify data in order to answer questions or recieve insights. However, those who are in the data science field can be the bridge and create web applications that allow other users to explore the data! A popular open-source Python library that is used to buildweb apps is Streamlit. [Streamlit](https://streamlit.io/) is easy to use and you can share our web app with others with a simple link! 

If you haven't use Streamlit before, you can follow this installation tutorial [here](https://docs.streamlit.io/get-started/installation). Once you've installed in on your computer, you can just import it as a library in Python! While I will showing my Streamlit app I created, I recommended watching this [video][https://www.youtube.com/watch?v=sogNluduBQQ] to get familiar with how it works.

### Designing the Pet Streamlit App
My dataset that I will be using is available to download on my [Github repository](https://github.com/clawmendra/petfinder). This data is filled with the profiles of pets available for adoption in Utah. Looking back at my motivating question, I want to compare the dog adoptions with the cat adoptions. I thought it would be best to create two new datasets, one with cats and one with dogs, and add two tabs to my web app where users can distinguish between these animals.

{%- highlight python -%}
# Use the streamlit library
import streamlit as st

# Filter by dogs and cats and create tabs
adoptions = pd.read_csv('animals_data.csv')

cats = adoptions[adoptions['species'] == 'Cat']
dogs = adoptions[adoptions['species'] == 'Dog']

tab1, tab2 = st.tabs(['Cats', 'Dogs'])

{%- endhighlight -%}

Now that I have my species tabs, I want to add some interactive features and visual aids that will allow the user to gain insights for each species. A great way to do this is to make a plot that changes depending on certain filters that are selected. 