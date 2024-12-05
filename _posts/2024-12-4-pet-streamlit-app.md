---
layout: post
title:  "Making a Web App to Uncover Pet Adoptions"
date: 2024-12-04
author: Almendra Clawson
description: "Using the data gathered from the Petfinder API to make a Streamlit App"
---

<p class="intro"><span class="dropcap">I</span>n this post, I’ll walk you through how I used the dataset gather from the  Petfinder API on adoptable pets to create a web app using Streamlit to explore the distribution of cats and dogs available for adoption in Utah. We'll cover everything from filtering the data to adding interactive features and visualizations that make it easy for anyone to gain insights into pet adoption trends.</p>

### Exploring our Petfinder Data

In my previous post, I used the free [Petfinder API](https://www.petfinder.com/developers/) to gather data to analyze the cats available for adoption in Utah. Now that I have a curated dataset with information on the pets available for adoption in Utah, I wanted to answer this question: How does the distribution of the dogs available for adoption compare to that of cats?

### Using Streamlit to Create a Web App

For those unfamiliar with programming or data science, modifying data to answer questions or gain insights can be challenging. However, data scientist can bridge this gap by creating web applications that allow other users to explore the data easily! 

A popular open-source Python library that is used to buildweb apps is [Streamlit](https://streamlit.io/). It's easy to use, and you can share our web app with others through a simple link! 

If you haven't use Streamlit before, you can follow this installation tutorial [here](https://docs.streamlit.io/get-started/installation). Once it's installed on your computer, you can just import it as a library in Python. While I'll be showing the Streamlit app I created, I recommended watching this [video](https://www.youtube.com/watch?v=sogNluduBQQ) to get familiar with how Streamlit works.

### Designing the Pet Streamlit App

All the code and dataset that I will be using is available to download on my [Github repository](https://github.com/clawmendra/petfinder). It contains profiles of pets available for adoption in Utah.

To answer my motivating question, I wanted to compare dog adoptions with cat adoptions. I decided to create two separate datasets—one for cats and one for dogs—and add two tabs to my web app to allow users to switch between these animals.

{%- highlight python -%}
# Use the streamlit library
import streamlit as st

# Filter by dogs and cats and create tabs
adoptions = pd.read_csv('animals_data.csv')

cats = adoptions[adoptions['species'] == 'Cat']
dogs = adoptions[adoptions['species'] == 'Dog']

tab1, tab2 = st.tabs(['Cats', 'Dogs'])

{%- endhighlight -%}

### Adding Interactive Features

Now that I have seperate tabs for each species, I wanted to add interactive features and visual aids to help users gain insights for each species. One effective way to do this is by creating a plot that changes based on selected filters.

I chose to filter the species by gender and age range. Streamlit offers several interactive elements, and I used a [radio](https://docs.streamlit.io/develop/api-reference/widgets/st.radio) button for the gender filers and a [multiselect](https://docs.streamlit.io/develop/api-reference/widgets/st.multiselect) widget for the age filter.

Here's how it looks in Python:

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

And here's how it looks in the app:

<figure> <img src="{{site.url}}/{{site.baseurl}}/assets/img/widgets-st.png" alt=""> <figcaption> Figure 1. - Gender and Age Streamlit Widgets.</figcaption> </figure>


### Adding Plots to Streamlit App

A wise professor taught me, "If you can create it in Python, you can create it on Streamlit." As shown in my code above, I save the user-selected widget values as variables (age_selected and gender_option). These input variables can then be used to create a plot that dynamically updates pbased on user selections.

I recommend creating a function that takes in the DataFrame and filter variables as arguments, generates a plot, and returns the figure. You can then display it using [st.plotly_chart()](https://docs.streamlit.io/develop/api-reference/charts/st.plotly_chart).

{%- highlight python -%}
cat_fig = animal_plot(df=cats, sex=gender_option, ages=age_selected)
st.plotly_chart(cat_fig)
{%- endhighlight -%}

### Using the Pet Adoption Web App
You can access the Streamlit app I created [here](https://clawmendra-petfinder-st-pet-mmw1ml.streamlit.app/). Some interesing insights I discovered with this app:
* There are more male cats available for adoption than male dogs.
* The most common age range for cats is "Baby" (kittens), with 117 available, compared to only 19 male puppies.
* A similar trend appears for females, with 64 female kittens available but only 12 puppies.

### Closing Remarks

What other insights can you gain from exploring the app? After checking it out, I encourage you to use the same dataset to create additional features with Streamlit. For example, you could add a table displaying summary statistics or incorporate other visualizations!