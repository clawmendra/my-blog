---
layout: post
title:  "Connecting the Dots with Business Questions and the Classroom"
date: 2024-10-03
author: Almendra Clawson
description: A tutorial post on how to map business questions into a data science process.
---

<p class="intro"><span class="dropcap">I</span>n this post, I share my experience transitioning from student to data analyst, tackling real-world problems at BYU Broadcasting. From navigating a competitive internship search to working with The Lisa Show team, I discuss how I applied classroom knowledge to solve business challenges using data. Along the way, I learned the importance of mapping out a clear process to tackle complex projects, and I share insights into the data science framework that helped me succeed.</p>


### Urgency to Apply my Knowledge

In Fall 2023, I knew it was time to look for internships before graduating the following year. The job market seemed tough, with too many applicants and too few positions. I applied on platforms like LinkedIn, Handshake, and Indeed, but mostly got rejection emails, which added to my anxiety. Beyond the resume boost, I needed an internship to apply the skills I had learned with real-life data before they faded from my memory. 

### Opportunity Arises at BYU Broadcasting

By April 2024, I heard about an opportunity at BYU Broadcasting through my statistical modeling class. After two rounds of interviews, I was thrilled to receive an offer for a hybrid data analyst/data engineer position on the Business Intelligence Team (BIT). I started in May and began learning tools like [DOMO](https://www.domo.com/?igaag=88996337689&igaat=&igacm=274253666&igacr=601617286958&igakw=domo&igamt=e&igant=g&utm_source=google&utm_medium=paidsearch&campid=701Vq000001zoWVIAY&gcreative=601617286958&gdevice=c&gnetwork=g&gkeyword=domo&gplacement=&gmatchtype=e&gtarget=&gadposition=&s_kwcid=AL!5964!3!601617286958!e!!g!!domo&gad_source=1&gclid=Cj0KCQjw99e4BhDiARIsAISE7P-wNDtsig3o9ByzxCAMclt3XMfR9XUn3SfycEemohi03VtweDY4F04aAq_GEALw_wcB) and [AWS](https://aws.amazon.com/free/?gclid=Cj0KCQjw99e4BhDiARIsAISE7P-QkSmpDsPoUowCf8XWYWPgtgtJr7V8MuiyNkGcCKyXj6uLAIcrS8caAuxCEALw_wcB&trk=6a4c3e9d-cdc9-4e25-8dd9-2bd8d15afbca&sc_channel=ps&ef_id=Cj0KCQjw99e4BhDiARIsAISE7P-QkSmpDsPoUowCf8XWYWPgtgtJr7V8MuiyNkGcCKyXj6uLAIcrS8caAuxCEALw_wcB:G:s&s_kwcid=AL!4422!3!651751059780!e!!g!!aws!19852662197!145019195897). Thankfully, my recent coursework (e.g. Intro to Machine Learning, Data Science Ecosystems, Statistical Modeling in R) gave me a solid foundation to build on.

### Meeting The Lisa Show Team

One of my responsibilities is working with [The Lisa Show](https://www.byuradio.org/the-lisa-show), a BYU Radio podcast hosted by Lisa Valentine Clark. My job is to help them answer questions about their audience and extract insights from their data. During my first meeting with the production team, I took notes on what they wanted to know in order to grow their audience. Translating their goals into data problems was my first real challenge.

<figure>
	<img src="{{site.url}}/{{site.baseurl}}/assets/img/lisa_show.jpg" alt="" style="width: 30%;"> 
	<figcaption>Figure 1 - The Lisa Show: Found on BYU Radio, Apple Podcasts, and Spotify.</figcaption>
</figure>

### Translating the Classroom to the Business World
With any solving business problem, having a some sort of structure for your data science process will help you keep track of what your objective should be. In class, every project was clearly laid out by professors but I needed to find my own outline on what I need to derive for The Lisa Show Team. From talking to my other co-workers, I learned from their work experience this structure of how to turn their questions into solutions derived from the data.

##### Step 1: Identify the problem and from into questions.
From the meeting, I distilled their concerns into three key questions.
- Does the audience enjoy the series/season layout for episodes?
- Which series are more popular and why?
- Is there a connection between popular posts/reels and increased listeners?

##### Step 2: Collect the data
After narrowing the questions I needed to answer, I needed to the collect and gather data. I knew that I needed data that contained information about their social media engagements on Facebook and Instagram. I also needed data on their listeners from not only BYU Radio but from third party platforms on Spotify and Apple Podcasts. Luckily for me, I had access to most of the data I needed already so I found which tables I wanted and combined them with the ETL tool in DOMO.

##### Step 3: Clean and wrangle the data
In DOMO, I looked for missing values and standardized the data by making sure that the datatypes were correct (e.g. 129 is an integer rather than a string). 

##### Step 4: Exploratory Data Analysis (EDA) 
With step 3 and 4, I found that these steps are often interwined with eachother. I made some basic visualizations to spot patterns in the data and to see if I had any missing or outlier values. Here's an example of a bar chart I made looking at their engagements with their Instagram account.

<figure>
	<img src="{{site.url}}/{{site.baseurl}}/assets/img/lisa_eda.jpg" alt=""> 
	<figcaption>Figure 2 - Basic bar chart made from The Lisa Show with DOMO. </figcaption>
</figure>

##### Step 5: Make models and interpret the data
Apply machine learning methods like supervised, unsupervised, or time series analysis. Interpret and deploy: Choose the best models, present findings clearly.

This process is pretty common among the data science world. Although this model differs, here's an image of another example that you can follow:

<figure>
	<img src="{{site.url}}/{{site.baseurl}}/assets/img/data-science-process.jpg" alt=""> 
	<figcaption>Figure 3. - This is another example of this process from appinventiv.com</figcaption>
</figure>

### Now What?
This process keeps me focused and on track, though I’ve learned it’s not always linear. Jumping between steps—like going back to clean data while modeling—is common, and that’s okay. I’m still working through Step 5 for The Lisa Show, but having this process outlined has helped me manage my time and expectations. If you're taking on a project for work, I recommend using this structure to stay organized. If you don't have an internship or a job that allows you the opportunity to apply this process, I invite you to come up with your own project. Form your own question and look for datasets online that you could use to start this process. Having practice working with this data science process with personal projects is great to have, especially if you don't have much related job experience to put on your resume.