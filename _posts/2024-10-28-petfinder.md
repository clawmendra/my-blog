---
layout: post
title:  "Using the Petfinder API to Analyze Animals"
date: 2024-11-11
author: Almendra Clawson
description: Insert description here
---

<p class="intro"><span class="dropcap">T</span>his post will describe how to create a blog post with the proper naming conventions, as well as tips for including images and links.  At the end there is a troubleshooting guide that can help with the most common problems .</p>


### Love for Pets

Throughout my childhood, I was surrounded with all sorts of pets. I pretty much had any type of pet that you could domesticate: cats, dogs, hamsters, birds, fish, and even hermit crabs. My pets were a source of love and companionship that I had that helped me with the trials that my family faced. When I got married and moved out of my home to study at BYU-Idaho University, I was diagnosed with depression and anxiety. Along with the support of counseling and medication, I wanted to adopt an emotional support animal to help my mental health. I looked online to see where I could adopt a cat near me and came across the website Petfinder.

### What is Petfinder?

[Petfinder](https://www.petfinder.com/) is one of the largest online, searchable databases used to promote pets in your area that are available for adoption. U.S. Shelters and adoption organizations can use this technology to maintain their own pet database and create profiles for their pets. Petfinder also allows those looking to adopt to create a profile to share information on what type of pet they are looking for to match with compatible pets based on factors like species, breed, age, good with kids, etc. Because of Petfinder, I was able to find a match and adopt my cat, Sophie. Petfinder had all the information I needed to narrow down which cats were available near me with the traits I needed for an emotional support animal. Although I am not looking for another cat right now, I'm interested with analyzing Petfinder's data to see which pet organization near me has a higher proportion of cats available to adopt than dogs?

### Using the Petfinder API

Petfinder has a free [RESTful](https://www.geeksforgeeks.org/rest-api-introduction/) API available to the public which you can access [here](https://www.petfinder.com/developers/). All it takes is a Petfinder account (which you can easily create) and request form to briefly state your intentions for using it. Once you've done completed that step, you will recieve a Secret key and an API key--which in this case is called "Client ID", this will enable you to use the information from Petfinder's servers.

The Petfinder API uses OAuth for authentication. Before we try to access the endpoint we need to get our access token. Using our Client/API key and our Secret, we can the requests library in Python to grab grab our access token and save it as a variable.

## Code Snippet
{%- highlight python -%}

client_id = 'insertAPIkeyhere'
client_secret = 'insertSecrethere'
auth_url = 'https://api.petfinder.com/v2/oauth2/token'
auth_data = {
    'grant_type': 'client_credentials',
    'client_id': client_id,
    'client_secret': client_secret
}

response = requests.post(auth_url, data=auth_data)
token = response.json().get('access_token')
{%- endhighlight -%}

### Accessing the endpoints in the Petfinder API

Now that we have access to use the Petfinder API, we can now access any endpoint and collect the data we want. 
Since I want to know what animals are available in organizations near me, I need to use the "animals" endpoint and the "organization" endpoint to gather the information I need.
Let's start with the "animals" endpoint. We need to use our access token as our header and adjust the parameters according to my question of interest. You can adjust the parameters
anyway you'd like, but I'm going to put my zipcode and search for available animals within 100 miles. I will also put a limit of 50 which will limit the number of results to return per page.

{%- highlight python -%}
headers = {
    'Authorization': f'Bearer {token}'
}
params = {
    'location': 'insert your zipcode here',
    'distance': 100, #miles
    'limit': 50           
}
{%- endhighlight -%}
{%- highlight python -%}
You can choose how many animals you want, but since I'm doing a limit of 50 pets per page, I'm gathering 8 pages of information which will give me a selection of 400 pets to filter through.


#Fetch multiple pages
all_animals = []
page = 1
max_pages = 8

while page <= max_pages:
    params['page'] = page
    response = requests.get('https://api.petfinder.com/v2/animals', headers=headers, params=params)

    if response.status_code == 200:
        animals_data = response.json()['animals']
        
        if not animals_data:
            break

        for animal in animals_data:
            record = {
                'organization_id': animal.get('organization_id'),
                'id': animal.get('id'),
                'species': animal.get('species'),
                'name': animal.get('name'),
                'age': animal.get('age'),
                'breed': animal.get('breeds', {}).get('primary'),
                'mixed': animal.get('breeds', {}).get('mixed'),
                'color': animal.get('colors', {}).get('primary'),
                'fixed': animal.get('attributes', {}).get('spayed_neutered'),
                'house_trained': animal.get('attributes', {}).get('house_trained'),
                'good_with_children': animal.get('environment', {}).get('children'),
                'good_with_dogs': animal.get('environment', {}).get('dogs'),
                'good_with_cats': animal.get('environment', {}).get('cats'),
                'gender': animal.get('gender'),
                'distance': animal.get('distance'),
                'url': animal.get('url')            
            }
            all_animals.append(record)
        
        page += 1 
    else:
        print("Error:", response.status_code, response.json())
        break

#Make it a dataframe
animals_df = pd.DataFrame(all_animals)
{%- endhighlight -%}


### Matching the Animals to their organization

With my new dataframe, I also have all the information I need. However, with the "animals" endpoint
I don't have have the names of the organizations where the pets are located. We have the organization ID
number which we can gather their names using the "organizations" endpoint. We can grab all the unique values
of orgnization IDs from the animals dataframe we made and loop though each value and grab their name from this
endpoint.

{%- highlight python -%}
org_ids = animals_df['organization_id'].unique()
org_names = {}

for id in org_ids:
    org_response = requests.get(f'https://api.petfinder.com/v2/organizations/{id}', headers=headers)
    if org_response.status_code == 200:
        org_data = org_response.json().get('organization', {})
        org_names[id] = org_data.get('name')
    else:
        print(f"Error fetching organization {id}")
{%- endhighlight -%}

Once we've done that, we have a table with all the information we need!


### Summarizing and Exploring the DataFrame

Forewarning, the Petfinder API is updated daily so the data changes quite a bit which makes sense due to pets being adopted or more being placed for adoption. However, we can use the same methods to summarize our dataset.

If you would like to know the how many rows and columns are in your dataframe, you can use ".shape" attribute which will return a tuple of (rows, columns). To see the datatypes of each columns in the dataframe, ou can use the attribute ".columns."
{%- highlight python -%}

animals_df.shape

animals_df.columns

summary_stats = {
    'Total Animals': len(animals_df),
    'Species Distribution': animals_df['species'].value_counts(),
    'Age Groups': animals_df['age'].value_counts(),
    'Most Common Breeds': animals_df['breed'].value_counts().head(),
    'Gender Distribution': animals_df['gender'].value_counts(normalize=True),
    'Percentage of Animals Fixed': (animals_df['fixed'] == True).mean() * 100,
    'House Trained Percentage': (animals_df['house_trained'] == True).mean() * 100,
    'Most Common Colors': animals_df['color'].value_counts().head(),
    'Organizations Count': animals_df['organization_name'].nunique()
}

print(summary_stats)

{%- endhighlight -%}
