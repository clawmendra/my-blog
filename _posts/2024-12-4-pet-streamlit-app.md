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

If you haven't use Streamlit before, you can follow this installation tutorial [here](https://docs.streamlit.io/get-started/installation). Once you've installed in on your computer, you can just import it as a library in Python! While I will showing my Streamlit app I created, I recommended watching this [video](https://www.youtube.com/watch?v=sogNluduBQQ)to get familiar with how it works.

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

Some filters I wanted to filter the species by gender and by age range. There are several kinds of interactive elements you can create with Streamlit. I decided to make the gender filter a [radio](https://docs.streamlit.io/develop/api-reference/widgets/st.radio) button, which is a basic select checkbox. With the age, I decided to make it a [multiselect](https://docs.streamlit.io/develop/api-reference/widgets/st.multiselect) widget which is basically a drop down bar shows the values that you can select. 

This is what it looks like in Python...

{%- highlight python -%}
with tab1:
    age_selected = st.multiselect(
        "Select Age Range for Cats",
        ["Baby", "Young", "Adult", "Senior"]
    )
    genders = ['Male', 'Female']
    gender_option = st.radio(
        "Gender for Cat",
        genders
    )
{%- endhighlight -%}

...and this is what it looks like on the app!
<figure> <img src="{{site.url}}/{{site.baseurl}}/assets/img/widgets-st.png" alt=""> <figcaption> Figure 1. - Gender and Age Streamlit Widgets.</figcaption> </figure>


### Adding Plots to Streamlit App
A wise professor taught me, "If you can create it in Python, you can create it on Streamlit." As you might have noticed in my code above, I saved all my widgets into variables (age_selected, genders). I can use these input variables to create a plot that is dependent on these inputs. I recommend creating a function that has the arguments of your dataframe and your variables to make a plot and then returns the figure. Once you've made this function, you can save it as a variable and then use [st.plotly_chart()](https://docs.streamlit.io/develop/api-reference/charts/st.plotly_chart) to plot it. 

{%- highlight python -%}
cat_fig = animal_plot(df=cats, sex=gender_option, ages=age_selected)
st.plotly_chart(cat_fig)
{%- endhighlight -%}

### Using the Pet Adoption Web App
You can access the Streamlit app I made [here](https://clawmendra-petfinder-st-pet-mmw1ml.streamlit.app/). Some insights I discovered with this app, I found there are more male cats available for adoption than male dogs. The most common age range for cats are kittens (labeled "Baby") 117 while their are only 19 male puppies available. When I switched to female, I saw the similar trend with 64 female kittens available for adoption but only 12 puppies.

### Closing Remarks
What other insights do you gain by looking at the app? After you look at my app, I encourage you to use that same dataset to create some other features using Streamlit. Perhaps you can see if you can add summary statistics table to the app! 