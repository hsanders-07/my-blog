---
layout: post
title:  "Analyzing the Perfect Season"
description: A deep, statistical look into what lead to Utah's undefeated 2008 football season
image: "/assets/img/utah_football_pic.avif"
display_image: false
---


<p class="intro"><span class="dropcap">T</span>he 2008-09 football season was arguably the best in program history for the University of Utah. Going 13-0 with the final game being against a young Nick Saban Alabama team in the Sugar Bowl, was a huge step forward for the program and bolstered Head Coach Kyle Whitingham's reputation. Obviously, going undefeated tells you a lot about how well the team performed, but what more can we learn about what lead to their success? Where did they thrive statistically in comparison to their opponents? These are the questions I will be answering in this post along with showing you how I did so! </p>


### Ethical Data Gathering?
Before I can get into why the method of data gathering I used was legal and ethical, I should probably first tell you where it is I got my data. I knew there had to be multiple options for gathering college football data so I did some researching until I found this [site](https://collegefootballdata.com/). Now, if you're not familiar with modes of data gathering, you might be thinking right about now something along the lines of, "Okay Hunter, so what, you just went to this site and copied and pasted the data they show? That seems a little sketchy." Rest assured though, that is not what I did! Rather this is a website that is made for the intended purpose of people getting their data. That's what they want you to do! I will get into the "How" of my data gathering in the next section, but the point I am trying to get accross here in this section is that I followed the instructions and paths this website provides to utizile their API and get my data. All being perfectly legal and ethical seeing that I followed their instructions to do so.

### How I Gathered the Data
As with most services, there are free ways to gather data through most APIs but also some things that you must pay to have access to. I found an option that didn't require anything other than me setting up a free account and thus getting my own personal API key. If you aren't sure what this is, it is essentially a code that you get once you sign up and use to get you access to their data. From here, this API was actually super easy to use. You are able to identify the data you are looking for and it will provide you with the url. From here you simply need to write code that takes that url and your API key to go and request the data. The code chunk below shows how I accomplished this.

{%- highlight python -%}
with open('cfb_apikey.txt', 'r') as file:
    apikey = f"Bearer {file.read()}"
url = yoururl.com
headers = {
    "Authorization": apikey,
    "Content-Type": "application/json"
    r = requests.get(url, headers=headers)
}
{%- endhighlight -%}
### Summary of What the Statistics Say

### Where You Can Get Further Information

### Where to Find My GitHub Repo for my Analysis
If you are interested in taking a deeper look into how I performed all the data gathering, cleaning, and analyzing, you are welcome to take a look at this [repository](https://github.com/hsanders-07/post_2_code) which contains it all.
