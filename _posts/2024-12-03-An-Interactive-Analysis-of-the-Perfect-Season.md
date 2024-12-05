---
layout: post
title:  "An Interactive Analysis of the Perfect Season"
description: A look into some of the highlights of my analysis of the 2008 Utah football season along with access to an interactive analysis app!
image: "/assets/img/sugar-bowl.jpg"
display_image: false
---


<p class="intro"><span class="dropcap">I</span>f you have taken a look at my previous blog post entitled "Analyzing the Perfect Season", then you will find this post to be a summary of some of the more interesting findings from my analysis of the University of Utah's 2008 football season. If you have not yet checked out that post, this will be a nice sample for you and hopefully intrique you enough to go check it out as well! Along with a summary of the statistics, I will also provide you with a link to an app I created where you can interact with the data yourself! </p>

### Motivation
As a lifelong Utah football fan, I’ve supported them through every game they’ve played. The 2008 season was nothing short of remarkable, and I’ve always been in awe of their success that year. This inspired me to dive deeper into the data from their games to uncover what made them so dominant. There were a lot of different datasets that I could've chosen to look at from the [college football API](https://collegefootballdata.com/) that I used, but I decided to look at the data from each of the offensive and defensive possesions they had during their regular season games. I set out to answer questions such as these:
<ul style="list-style-type:circle">
<li>Was their offense the main reason why they won games?</li>
<li>Was it their defense?</li>
<li>Maybe even a combo of the two?</li>
</ul>
I set out to see what I could find.

### Code Reference
The analysis required substantial coding to collect, clean, and organize the data. To see this code and get an idea of the things I had to do, you are welcome to check out this [repository](https://github.com/hsanders-07/post_2_code) which also contains the complete dataset that I started out with. 

### Some of my Findings
There were various different correlations and comparisons that chose to take a look at, but here I will simply provide you with some of my favorite findings. 
One of the comparisons I wanted to take a look at was yards gained vs starting yards to goal—essentially, how far the team was from the end zone when they began their drive. To gain some insight on this, I created two plots: one for all of Utah’s offensive drives and another for their defensive possessions.

<figure>
	<img src="https://hsanders-07.github.io/my-blog/assets/img/yards_vs_togo1.png" alt=""> 
</figure>

<figure>
    <img src="https://hsanders-07.github.io/my-blog/assets/img/yards_vs_togo2.png" alt="">
</figure>

Here's what these plots tell us:
<ol>
<li>Offense: Utah’s offensive productivity often forced opponents to start their drives with 70+ yards to go, creating a significant disadvantage for their opponents.</li>
<li>Defense: Utah’s defense rarely allowed opponents to get first downs. The dashed line at 10 yards gained highlights how often Utah forced 3-and-outs, thus prevented even a single first down.</li>

Overall, we can clearly see that Utah had a rather dominant offense that was able to capitalize on having the ball with their ability to storm down the field and score touchdowns with little evidence suggesting they were limited when starting far from the endzone. 
Alternatively, Utah's defense was also rather dominant as they were able to really hinder their opponents' ability to score touchdowns and managed to use yards to goal to their advantage.

### Take a Look for Yourself!

These examples are just the tip of the iceberg.  It is time for you to get your hands dirty in this data and see what other insights you can discover. I built this [streamlit app](https://utah-football-analyzer.streamlit.app/) to allow you the chance to interact with the data. You are able to select the variable(s) you want to analyze and whether the data is from Utah on offense or defense.

The two types of visuals you will be able to produce are scatterplots and boxplots. The scatterplots are to allow you to see the relation between the two variables of your choosing and the boxplots are to allow you to compare the difference between a specific variable, also of your choosing, for when Utah is on offense and for when they are on defense.

In my full analysis, there were still some variable relations that I did not explore that you can go and learn about! For example, you could take a look at the spread of the data for start_yards_to_goal (using the boxplot) and learn about the how well Utah controled field position. Another example of something you could look into is the trend for start_yards_to_goal vs plays and see just how impactful having more yards to go is on how many plays they had that possession. The options are endless! OK... not quite, but there are a good amount!

Here's a quick reference for definitions of the variables you'll see in the app:

| Variable      | Description |
| ----------- | ----------- |
| Offense      | The team with the ball       |
| Defense  | The team without the ball        |
| Scoring      | 1 if they score on the drive, 0 if they do not       |
| Elapsed   | Time in minutes and portion of a minute the offense had the ball        |
| Plays      | How many individual plays they ran       |
| Start yards to goal  | How far away they started from the end-zone        |
| Yards      | How many yards they gained       |
| Off points gained   | Net points gained by the offense        |

### Wrap Up
I hope this post and the interactive app provide you with new insights into Utah’s incredible 2008 season. It’s remarkable to see how a combination of offensive and defensive dominance led to such a historic run. Who's to know if/when Utah will have another season quite like this one, but one thing is for sure, if they want any hope of this kind of a successful season again they will need to dominate on both sides of the ball the way they did in 2008. 

Who is one of your favorite teams and what year was your favorite as a fan? I challenge you to go find data on that team and year and see what you can find about what lead to their success! Best of luck!