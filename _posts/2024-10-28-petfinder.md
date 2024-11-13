---
layout: post
title:  "Using the Petfinder API to Analyze Animals"
date: 2024-11-11
author: Almendra Clawson
description: Insert description here
---

<p class="intro"><span class="dropcap">T</span>his post will describe how to create a blog post with the proper naming conventions, as well as tips for including images and links.  At the end there is a troubleshooting guide that can help with the most common problems .</p>


### Love for Pets

Throughout my childhood, I was surrounded with all sorts of pets. I pretty much had any type of pet that you could domesticate: cats, dogs, hamsters, birds, fish, and even hermit crabs. My pets were a source of love and companionship that I had that helped me with the trials that my family faced. When I got married and moved out of my home to study at BYU-Idaho University, I was diagnosed with depression and anxiety. Along with the support of counseling and medication, I wanted to adopt an emotional support animal to help me as well. I looked online to see where I could adopt a cat near me and came across the website Petfinder.

### What is Petfinder?

[Petfinder](https://www.petfinder.com/) is one of the largest online, searchable databases used to promote pets in your area that are available for adoption. U.S. Shelters and adoption organizations can use this technology to maintain their own pet database and create profiles for their pets. Petfinder also allows those looking to adopt to create a profile to share information on what type of pet they are looking for to match with compatible pets based on factors like species, breed, age, good with kids, etc. Because of Petfinder, I was able to find a match and adopt my cat, Sophie. Petfinder had all the information I needed to narrow down which cats were available near me with the traits I needed for an emotional support animal. Although I am not looking for another cat right now, I'm interested with analyzing Petfinder's data to see which pet organization near me has a higher proportion of cats available to adopt than dogs?

### Accessing the Petfinder API

Petfinder has a free [RESTful](https://www.geeksforgeeks.org/rest-api-introduction/) API available to the public which you can access [here](https://www.petfinder.com/developers/). All it takes is a Petfinder account (which you can easily create) and request form to briefly state your intentions for using it. Once you've done completed that step, you will recieve a Secret key and an API key--which in this case is called "Client ID", this will enable you to recieve information from Petfinder's servers.