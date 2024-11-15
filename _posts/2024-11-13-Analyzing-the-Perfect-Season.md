---
layout: post
title:  "Analyzing the Perfect Season"
description: A deep, statistical look into what led to Utah's undefeated 2008 football season
image: "/assets/img/utah_football_pic.avif"
display_image: false
---


<p class="intro"><span class="dropcap">T</span>he 2008-09 football season was arguably the best in program history for the University of Utah. Obviously, going undefeated tells you a lot about how well the team performed, but what more can we learn about what lead to their success? Where did they thrive statistically in drive statistics comparison to their opponents'? These are the questions I will be answering in this post along with showing you how I did so! </p>

### Ethical Data Gathering?
I knew there had to be multiple options for gathering college football data so I did some research until I found this [site](https://collegefootballdata.com/). Now, if you're not familiar with modes of data gathering, you might be thinking right about now something along the lines of, "Okay Hunter, so what, you just went to this site and copied and pasted the data they show? That seems a little sketchy." Rest assured, that is not what I did! Rather this is a website that is made for the intended purpose of people getting their data. That's what they want you to do! So essentially, as long as you get your own API key and follow their instructions, you can be sure that you're following the laws and ethics of data gathering.

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
Upon obtaining all of the data I requested, some data cleaning and reorganization were needed for me to do the analysis I was looking to do. I won't go over what all I did to get the data ready, but if you are curious, I have my code repository linked at the end of this post. 

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

Now we are ready to dive into the Exploratory Data Analysis! In order to have an idea of what variables we should explore deeper, we need to know how they relate together. A correlation matrix is perfect for this. 


<figure>
	<img src="https://hsanders-07.github.io/my-blog/assets/img/ute_off_corr.png" alt=""> 
</figure>

<figure>
    <img src="https://hsanders-07.github.io/my-blog/assets/img/ute_def_corr.png" alt="">
</figure>

We can immediately start to see a difference in various correlations from when Utah is on offense vs when they are on defense. Offensively, they were clearly able to find more success than their opponents were. We can see this further by looking at the data points of yards vs starting_yards_to_goal. Here are the two graphs to visualize the correlation that was calculated.

<figure>
	<img src="https://hsanders-07.github.io/my-blog/assets/img/yards_vs_togo1.png" alt=""> 
</figure>

<figure>
    <img src="https://hsanders-07.github.io/my-blog/assets/img/yards_vs_togo2.png" alt="">
</figure>

The two main things we can learn from these graphs is that Utah's offensive productivity made life difficult on their opponent's offense due to the vast majority of their drives having 70+ yards to go. We also learn that the Utah defense were not fans of their opponents getting first downs. I put the dashed line at the 10 yards gained point in the x-axis to show just how often the Utah defense forced a 3-and-out, or kept the other team from getting even a single first down.

Finally, I would like to just take a look at some simple average comparisons. I will show you the code of how I got these averages. You will see this if you look at my coding repository, but just so you know incase you don't, "numeric_df" is the data for when Utah was on offense and "numeric_df2" is for when they were on defense. From these averages, it is clear that Utah held a significant statistical advantage on offense and defense in some of these very crucial statistics.

{%- highlight python -%}
print(f"Utah's average time on offense was: {numeric_df['elapsed'].mean()}")
print(f"Utah's average time on defense was: {numeric_df2['elapsed'].mean()}")

print(f"Utah's average offensive points gained was: {numeric_df['off_points_gained'].mean()}")
print(f"Utah's opponents average offensive points gained was: {numeric_df2['off_points_gained'].mean()}")

print(f"The proportion of Utah's drives ending with points was: {numeric_df['scoring'].mean()}")
print(f"The proportion of Utah's opponent's drives ending with points was: {numeric_df2['scoring'].mean()}")

#=> prints:
Utah's average time on offense was: 2.6599099099099095
Utah's average time on defense was: 2.0763440860215057
Utah's average offensive points gained was: 2.391891891891892
Utah's opponents average offensive points gained was: 1.070967741935484
The proportion of Utah's drives ending with points was: 0.4864864864864865
The proportion of Utah's opponent's drives ending with points was: 0.23870967741935484
{%- endhighlight -%}


### All the Little Details
Overall, we have discovered some really cool things. We learned that it wasn't just the Utah defense that statistically dominated, but their offense as well. My challenge to you is to go analyze a season of your favorite team and share what you discover!

If you want to get more information on the data of the API that I used or know where I went to ensure data accuracy, you can you the same links that I did. The website for the API that I used was this [site](https://collegefootballdata.com/). Here you can also find all the information you would need to run your own API requests such as syntax and API instructions. The only other site I used was [ESPN](https://www.espn.com/college-football/team/schedule/_/id/254/season/2008). That is where you can find ESPN's data of each game and see the play-by-play which matches the data I used.

If you are interested in taking a deeper look into how I performed all the data gathering, cleaning, and analyzing, you are welcome to take a look at this [repository](https://github.com/hsanders-07/post_2_code) which contains it all.
