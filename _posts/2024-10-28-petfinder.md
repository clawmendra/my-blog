---
layout: post
title:  "Using the Petfinder API to Analyze Cats"
date: 2024-11-11
author: Almendra Clawson
description: "Learn how to use the Petfinder API to analyze pet adoption data."
---

<p class="intro"><span class="dropcap">A</span>re you interested in understanding pet adoption trends in your area? In this post, I’ll show you how I used the Petfinder API to analyze the availability of pets near me, specifically exploring which organizations have the highest proportion of cats available for adoption.</p>

### Love for Pets

Throughout my childhood, I was surrounded by pets: cats, dogs, hamsters, birds, fish, and even hermit crabs. My pets provided love and companionship, helping me cope during challenging times. When I moved out to study at BYU-Idaho University, I was diagnosed with depression and anxiety. Along with counseling and medication, I decided to adopt an emotional support animal. Looking online, I came across Petfinder, which helped me find my cat, Sophie. With my previous experience with using Petfinder, I wanted to analyze Petfinder’s data to see which pet organizations near me have a higher proportion of cats compared to dogs.

<figure> <img src="{{site.url}}/{{site.baseurl}}/assets/img/sophie.jpg" alt="" style="width: 30%;"> <figcaption> Figure 1. - My cat Sophie. Photo taken by me.</figcaption> </figure>

### What is Petfinder?

[Petfinder](https://www.petfinder.com/) is one of the largest online, searchable databases for pets available for adoption. Shelters and adoption organizations across the U.S. use it to list profiles for their animals, which potential adopters can filter by species, breed, age, temperament, and more. Petfinder allowed me to narrow down my options and find a cat that met my needs for an emotional support animal. Using Petfinder’s API, I aimed to answer the question: Which organizations near me have the highest proportion of cats available for adoption?

### Using the Petfinder API

Petfinder offers a free [RESTful](https://www.geeksforgeeks.org/rest-api-introduction/) API to the public, which you can access [here](https://www.petfinder.com/developers/). You’ll need to create a Petfinder account and submit a brief form explaining your intended use. Once approved, you’ll receive an API key (referred to as "Client ID") and a Secret key, which you’ll use to authenticate and access data.

The Petfinder API uses OAuth for secure access. First, we’ll retrieve an access token using our API key and Secret key with Python’s requests library, saving it as a variable for later requests.

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

### Accessing the Petfinder Endpoints

With our access token, we can access endpoints in the Petfinder API. To analyze available pets, we’ll use the "animals" and "organizations" endpoints. By specifying parameters like location and distance, I limited my search to 50 pets per page within a 100-mile radius. Here’s a sample of the setup:

{%- highlight python -%}
headers = {
    'Authorization': f'Bearer {token}'
}
params = {
    'location': 84606, # zipcode
    'distance': 100, # miles
    'limit': 50           
}
{%- endhighlight -%}

To gather a representative dataset, I retrieved 8 pages of results (400 pets in total) and stored them in a DataFrame.

{%- highlight python -%}
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
                'name': animal.get('name')
                #...Insert more values here you want to grab          
            }
            all_animals.append(record)
        
        page += 1 
    else:
        print("Error:", response.status_code, response.json())
        break

#Convert to a dataframe
animals_df = pd.DataFrame(all_animals)
{%- endhighlight -%}


### Adding Organization Name

With my new dataframe, I have all the information I need. However, with the "animals" endpoint
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


### Summarizing the Data

Since Petfinder updates daily, the data changes frequently. However, we can use the same methods to summarize our dataset.

If you would like to know the how many rows and columns are in your dataframe, you can use ".shape" attribute which will return a tuple of (rows, columns). To see the datatypes of each columns in the dataframe, you can use the attribute ".columns."
{%- highlight python -%}

animals_df.shape

animals_df.columns

{%- endhighlight -%}

To view some initial stats, I created a summary dictionary to check the distributions of pet species and age groups.

{%- highlight python -%}
summary_stats = {
    'Species Distribution': animals_df['species'].value_counts(),
    'Age Groups': animals_df['age'].value_counts()
    #...insert more here
}
{%- endhighlight -%}

For a full look at the code and statistics, see my [GitHub repository](https://github.com/clawmendra/petfinder). Here’s an overview of species and age distributions from the dataset:

#### Species Distribution

| Species     | Count       |
| ----------- | ----------- |
| Cat         | 216         |
| Dog         | 178         |
| Rabbit      | 4           |
| Duck        | 1           |
| Rat         | 1           |

#### Age Distribution

| Age Groups  | Count       |
| ----------- | ----------- |
| Baby        | 148         |
| Adult       | 128         |
| Young       | 107         |
| Senior      | 17          |

Using these summaries, I created a bar chart with Seaborn to visualize pet listings by organization, discovering that [OutReach Pawsibilites](https://outreachpawsabilitiesinc.org/) had the highest number of listings, with around 60 pets.
<figure> <img src="{{site.url}}/{{site.baseurl}}/assets/img/totalanimals.png" alt=""> <figcaption> Figure 2. - Bar Chart of Total Number of Pets created with Seaborn and Matplotlib.</figcaption> </figure>

### Exploring Cat-Only Organizations

Next, I focused on organizations with a higher proportion of cats. By filtering out organizations without cats and calculating the proportion of cats at each organization, I found that nine organizations listed only cats!

<figure> <img src="{{site.url}}/{{site.baseurl}}/assets/img/catprop.png" alt=""> <figcaption> Figure 3. - Bar Chart of Cat Proportions created with Seaborn and Matplotlib.</figcaption> </figure>

### Conclusion

If you’d like to explore the Petfinder API, I encourage you to use this approach to analyze the types of animals available near you. For example, you could investigate which organizations primarily list dogs.
Exploring the Petfinder API brought an interesting insight with the pets available for adoption in my area. Whether you are an aspiring data scientist, a pet lover, or both, I would encourage you to dive deeper into the API and uncover more!