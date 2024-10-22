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
With any solving business problem, having a clear structure for your data science process will helps you stay focused on the objective. In class, every project was clearly laid out by professors but for The Lisa Show, I needed to develop my own outline. From talking to my other co-workers, I learned how they turned business questions into data-driven solutions.

#### Step 1: Identify the problem and from into questions.
From the meeting, I distilled their concerns into three key questions.
- Does the audience enjoy the series/season layout for episodes?
- Which series are more popular and why?
- Is there a connection between popular posts/reels and increased listeners?

#### Step 2: Collect the data
After narrowing down the questions, I needed to gather the right data. I knew that I needed data on social media engagement from Facebook and Instagram, as well as listener data from BYU Radio, Spotify, and Apple Podcasts. Luckily, I had access to most of the data already, so I selected the relevant tables and combined them using DOMO's ETL tool.

#### Step 3: Clean and wrangle the data
In DOMO, I looked for missing values and standardized the data by ensuring that the datatypes were correct (e.g., 129 is an integer rather than a string).

#### Step 4: Exploratory Data Analysis (EDA) 
I found that data cleaning and EDA are often intertwined. I created basic visualizations to spot patterns in the data and to check for missing or outlier values. Here's an example of a bar chart I made of their Instagram engagement.

<figure>
	<img src="{{site.url}}/{{site.baseurl}}/assets/img/lisa_eda.jpg" alt=""> 
	<figcaption>Figure 2. - Basic bar chart made from The Lisa Show Sprout data in DOMO. </figcaption>
</figure>

#### Step 5: Model and interpret the data
In this step, you can apply machine learning methods like supervised learning, unsupervised learning, or time series analysis. After testing several models, we can interpret the results to find the best one that answers our initial questions. I am currently working on this step for The Lisa Show, but once I'm done, I’ll present my findings to the team!

### Now What?
This process is common in data science, although there are several versions of it. Here's another example of a similar framework:

<figure>
	<img src="{{site.url}}/{{site.baseurl}}/assets/img/data-science-process.jpg" alt=""> 
	<figcaption>Figure 3. - This is another example of this process from appinventiv.com</figcaption>
</figure>

While the process helps me stay focused, I’ve learned it’s not always linear. Jumping between steps—like returning to clean data while modeling—is common, and that’s okay. I’m still working through Step 5 for The Lisa Show, but having this process outlined has helped me manage my time and expectations.

If you're taking on a project at work, I recommend using this structure to stay organized. If you don’t have an internship or job that allows you to apply this process, I encourage you to come up with your own project. Form your own question and look for datasets online to start your process. Gaining experience with this framework through personal projects is invaluable, especially if you lack related work experience to highlight on your resume.

