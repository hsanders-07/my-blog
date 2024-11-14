---
layout: post
title:  "Analyzing the Perfect Season"
description: A deep, statistical look into what lead to Utah's undefeated 2008 football season
image: "/assets/img/utah_football_pic.avif"
display_image: false
---


<p class="intro"><span class="dropcap">T</span>he 2008-09 football season was arguably the best in program history for the University of Utah. Going 13-0 with the final game being against a young Nick Saban Alabama team in the Sugar Bowl, was a huge step forward for the program and bolstered Head Coach Kyle Whitingham's reputation. Obviously, going undefeated tells you a lot about how well the team performed, but what more can we learn about what lead to their success? Where did they thrive statistically in drive statistics comparison to their opponents'? These are the questions I will be answering in this post along with showing you how I did so! </p>


### Ethical Data Gathering?
Before I can get into why the method of data gathering I used was legal and ethical, I should probably first tell you where it is I got my data. I knew there had to be multiple options for gathering college football data so I did some researching until I found this [site](https://collegefootballdata.com/). Now, if you're not familiar with modes of data gathering, you might be thinking right about now something along the lines of, "Okay Hunter, so what, you just went to this site and copied and pasted the data they show? That seems a little sketchy." Rest assured, that is not what I did! Rather this is a website that is made for the intended purpose of people getting their data. That's what they want you to do! I will get into the "How" of my data gathering in the next section, but the point I am trying to get accross here is that I followed the instructions and paths this website provides to utizile their API and get my data. All being perfectly legal and ethical.

### How I Gathered the Data
As with most services, there are free ways to gather data through most APIs but also some things that you must pay to have access to. I found an option that didn't require anything other than me setting up a free account and thus getting my own personal API key. If you aren't sure what this is, it is essentially a code that you get once you sign up and use to get you access to their data. From here, this API was actually super easy to use. You are able to identify the data you are looking for and it will provide you with the url. From here you simply need to write code that takes that url and your API key to go and request the data. The code chunk below shows how I accomplished this.

{%- highlight python -%}
with open('cfb_apikey.txt', 'r') as file:
    apikey = f"Bearer {file.read()}"
url = "https://api.collegefootballdata.com/drives?seasonType=regular&year=2008&team=Utah"
headers = {
    "Authorization": apikey,
    "Content-Type": "application/json"
    r = requests.get(url, headers=headers)
}
{%- endhighlight -%}

### Summary of What the Statistics Say
Upon obtaining all of the data I requested, some data cleaning and reorgination were needed for me to do the analysis I was looking to do. I won't go over what all I did to get the data ready, but if you are curious, I have my code repository linked at the end of this post. 

To give you an idea of how I got the data to look, the following is the first five and last five instances, or in this case  "drives", of the season.

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>offense</th>
      <th>defense</th>
      <th>scoring</th>
      <th>elapsed</th>
      <th>plays</th>
      <th>start_yards_to_goal</th>
      <th>yards</th>
      <th>drive_result</th>
      <th>off_points_gained</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Michigan</td>
      <td>Utah</td>
      <td>0</td>
      <td>1.533333</td>
      <td>3</td>
      <td>71</td>
      <td>2</td>
      <td>PUNT</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Michigan</td>
      <td>Utah</td>
      <td>1</td>
      <td>2.133333</td>
      <td>4</td>
      <td>26</td>
      <td>26</td>
      <td>PASSING TD</td>
      <td>6</td>
    </tr>
    <tr>
      <td>Utah</td>
      <td>Michigan</td>
      <td>1</td>
      <td>3.700000</td>
      <td>8</td>
      <td>75</td>
      <td>75</td>
      <td>RUSHING TD</td>
      <td>6</td>
    </tr>
    <tr>
      <td>Michigan</td>
      <td>Utah</td>
      <td>1</td>
      <td>2.333333</td>
      <td>6</td>
      <td>50</td>
      <td>17</td>
      <td>FG GOOD</td>
      <td>3</td>
    </tr>
    <tr>
      <td>Utah</td>
      <td>Michigan</td>
      <td>1</td>
      <td>6.233333</td>
      <td>14</td>
      <td>77</td>
      <td>66</td>
      <td>FG GOOD</td>
      <td>3</td>
    </tr>
        <tr>
      <td>Utah</td>
      <td>BYU</td>
      <td>1</td>
      <td>0.066667</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
      <td>PASSING TD</td>
      <td>6</td>
    </tr>
    <tr>
      <td>BYU</td>
      <td>Utah</td>
      <td>0</td>
      <td>3.966667</td>
      <td>8</td>
      <td>75</td>
      <td>56</td>
      <td>INT</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Utah</td>
      <td>BYU</td>
      <td>1</td>
      <td>5.400000</td>
      <td>9</td>
      <td>29</td>
      <td>29</td>
      <td>PASSING TD</td>
      <td>6</td>
    </tr>
    <tr>
      <td>BYU</td>
      <td>Utah</td>
      <td>0</td>
      <td>0.533333</td>
      <td>4</td>
      <td>67</td>
      <td>13</td>
      <td>INT</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Utah</td>
      <td>BYU</td>
      <td>0</td>
      <td>2.100000</td>
      <td>4</td>
      <td>60</td>
      <td>0</td>
      <td>END OF GAME</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

From here you might be struggling to identify what each of these variables represent, so let me provide you a key for that as well.

| Variable      | Description |
| ----------- | ----------- |
| Offense      | The team with the ball       |
| Defense  | The team without the ball        |
| Scoring      | 1 if they score on the drive, 0 if they do not       |
| Elapsed   | Time in minutes and portion of a minute the offense had the ball        |
| Plays      | How many individual plays they ran       |
| Start yards to goal  | How far away they started from the end-zone        |
| Yards      | How many yards they gained       |
| Drive Result   | What happened at the end of the drive        |
| Off points gained   | Net points gained by the offense        |

Now we are ready to dive into the Exploritory Data Analysis! In order to have an idea of what variables we should explore deeper, we need to know how they relate together. A correlation matrix is perfect for this. 


<figure>
	<img src="https://hsanders-07.github.io/my-blog/assets/img/utah_corr_1.png" alt=""> 
    <img src="https://hsanders-07.github.io/my-blog/assets/img/utah_corr2.png" alt="">
</figure>

### Where You Can Get Further Information

### All the Little Details
If you are interested in taking a deeper look into how I performed all the data gathering, cleaning, and analyzing, you are welcome to take a look at this [repository](https://github.com/hsanders-07/post_2_code) which contains it all.
