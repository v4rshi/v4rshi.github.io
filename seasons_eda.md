
## **Soundtrack of Seasons**: Unraveling My Spotify Saga Over The Last 9 Years

**Project Description**: I was able to get playlist data for my Spotify playlists thanks to a website called [Exportify](https://exportify.net/). It made me wonder, can I use this data to understand my mood and well-being over the years based on the season of the year I listened to something and the sentiment of the songs (name and lyrics) themselves?

**Data**: My dataset spans from April 2016 to August 2024. Each entry contains rich metadata including artist, track, addition date, and genre. It also includes an attribute called 'Valence', which captures the sentiment of a song. Tracks with high valence sound more positive (happy, cheerful, euphoric), while tracks with low valence sound more negative (sad, depressed, angry). Read more about it [here](https://community.spotify.com/t5/Spotify-for-Developers/Valence-as-a-measure-of-happiness/td-p/4385221). 

**Motivation & Hypothesis**: This dataset captures a transformative period in my life. From relocating from Dubai to Indiana for college, navigating the global pandemic (and graduate school in lockdown), experiencing personal losses, moving to San Francisco, starting my career, meeting my now husband and getting married, and transitioning between jobs. Throughout these experiences, Spotify remained a constant companion.

I've observed that my playlists often serve as a form of musical journaling, reflecting my emotional state and circumstances. This project aims to analyze the evolution of my musical preferences over time and explore potential correlations between playlist characteristics (content, length, addition frequency) and my emotional state at the time. Valence is a cool attribute, but I think I want more nuance than a number - I want a clearly defined set of emotions associated with my musical history. 

Key focus areas for this project include: 

1. Temporal analysis of musical taste to confirm if the data reveals what I think know (or do not know) about my musical taste 
2. Seasonal patterns in playlist composition, particularly relative to seasons and whatever weather changes they bring
3. Sentiment analysis of song lyrics using LLM's, with a specific focus on the period of July 2023 to now (coinciding with my period of unemployment)

By examining these data points, I hope to uncover insights into how my music choices have mirrored my life experiences and emotional states during this pivotal time. 

##### **It is important to note that this data did not include how often I listened to specific songs, just when I added them to a given playlist. This data would be great for a more in-depth analysis of my listening patterns.**

---

<style>
  .zoom:hover {
    transform: scale(3);
    transition: transform 0.5s ease;
  }
</style>

## Findings and Visualizations: 
### NOTE: Hover over all graphs to see a bigger version of them! 

### 1. The first thing I looked at was who my most listened to artists were.
I was fully expecting my top artist to be Charli XCX but in a rather surprising turn of events, its Future??? I did not see this in my Future, that is for sure.

<img src="images/top_20_artists.png?raw=true" width="1000" class="zoom"/>

To dig into this deeper, I looked into when I added all the songs with Future on them... to find most of it was this year. 

<img src="images/future_breakdown.png?raw=true" width="1000" class="zoom"/>

That made Future being my top artist sense because this year was when "We Don't Trust You" and "We Still Don't Trust You" with Metro Boomin' and Future came out, and my husband and I had those albums on repeat most of this year and I ended up adding a bunch of songs by or featuring Future to my playlists this year. 

### 2. This summer is a BRAT summer for me - but historically was that always the case?
Looks like spring is BRAT green! Each season is quite different, winter seemingly being all over the place since Disney, Britney Spears and BTS are all on there! 

<img src="images/top_10_seasonal.png?raw=true" width="1000" class="zoom"/>

### 3. I chose to look at add number of songs over the years (by month and season) to see when I most actively added music to playlists

I was not surprised to see how erratic my playlist making was until 2022, which was when I started my first full-time job, after which I was not curating my music as intentionally (made sense as my work took up most of my time) and then in August 2024 there was a spike that can be explained by my coping with a stressful situation with music at the time.

<img src="images/monthly_adds_by_season.png?raw=true" width="1000" class="zoom"/>

### 4. I tried to visualize this differently with number of songs added by season over the years.

I hypothesized I would be most active in the winter and summer, but it is clear that the pandemic in 2020 and my time being unemployed in 2024 are when I am most active. This coincides with when I was going through a lot in my personal life, too. 

<img src="images/monthly_song_adds_by_season_linechart.png?raw=true" width="1000" class="zoom"/>


### 5. I wanted to then look at song-adding volume over the seasons. I tried to visualize this differently where I normalized my data by dividing each season by no. days in a season and then dividing that by the number of years in my dataset, 9 (WOW that is a long time). 

This made sense to me because overall I did feel I was most active in the winter as I generally was on break when I was in college but also when the weather was extreme and I spent too much time indoors - meaning I leaned on music more to pass time.

<img src="images/normalized_graph_2.png?raw=true" width="1000" class="zoom"/>

### 6. I tried visualizing seasonal distributions for various other music traits, like Danceability, Valence, Energy and Tempo, to get a general sense of what kind of music I liked in different seasons. 

This visual made it clear that my taste seems fairly consistent across the seasons but that overall I like songs that you can dance to, have high energy and high tempo! Ya girl like music she can have a good time to! 

<img src="images/other_trait_distribution.png?raw=true" width="1000" class="zoom"/>

### 7. I wanted to then look at the distributions by season and year it was added to a playlist (there are ~9 years worth of data!).

I chose to pay the closest attention to 2019-2020, 2023-2024 and see how they compared to one another. The rationale is as follows:

- 2020 was the year of the pandemic, and 2019 is a baseline to compare pre and post COVID-19 music preferences
  <img src="images/attributes19.png?raw=true" width="1000" class="zoom"/>
  <img src="images/attributes20.png?raw=true" width="1000" class="zoom"/>
  
- 2023 was the year I got married but 2024 was the year I was stuck without a job in a bad market
  <img src="images/attributes23.png?raw=true" width="1000" class="zoom"/>
  <img src="images/attributes24.png?raw=true" width="1000" class="zoom"/>

I did also break each year down into seasons to see any seasonal trends, but to not clutter this page with too many graphs I will summarize my observations below:

The shift in my music preferences between **2019 and 2020** shows a surprising trend towards, on average, more energetic and positive songs. While 2020 is often associated with the hardships of the COVID-19 pandemic, it was also the year I was unexpectedly admitted to graduate school. This personal triumph, especially significant given the closed borders and uncertainty, may explain my gravitation towards upbeat music. My experience highlights how individual circumstances can contrast with broader narratives during global events. 

Between **2023 and 2024**, my music preferences show a drop, on average, in all attributes except tempo. This shift aligns with the challenges I'm facing in 2024, particularly navigating a difficult job market. The decrease in most musical attributes likely reflects my current emotional state, while the increased tempo might indicate a need for motivation or energy during these stressful times. My playlist has essentially become a reflection of my professional struggles and associated emotions. 

Note to self: Either make these playlists private or start a new career as the world's most reluctant psychic. "For just $9.99, I'll predict your future by analyzing your 'Most Played' list!" Hmm, maybe I'm onto something here...

---

### 8. I thought it would be interesting to see what my top 10 genres were by season and if they varied at all.
 In short, barely. I still am basic as hell and listen to a lot of pop, however the genres following that moved around but were only edm, hip hop, rap and/or some pop variation. What was surprising to me was the random appearance of 'Modern Rock' in the Wintertime. Wintertime House of Blues, I guess?

<img src="images/top_10_genres_by_season.png?raw=true" width="1000" class="zoom"/>

I then tried to visualize this differently with a stacked bar chart and over the top 20 genres overall

<img src="images/top_genres_by_season_barplot.png?raw=true" width="1000" class="zoom"/>

### 9. I wondered, do I like current releases or nostalgic music more, and does this vary by season?
The boxplot graph below shows how my music listening habits change throughout the year. It compares the age of songs I listen to (how long ago they were released compared to when it was added to a playlist) across different seasons. The insights were very interesting. 

A primer on what a boxplot even is: it is a simple visual tool that shows the spread and symmetry of a dataset by dividing it into quartiles and highlighting key statistics like the median and potential outliers. It uses a box to represent the middle 50% of the data and lines extending from the box to show the range, making it easy to see how data is distributed. Feel free to also refer to [this guide](https://www.simplypsychology.org/boxplots.html) on how to interpret boxplots.

<img src="images/currentn_v_nostalgic_boxplot.png?raw=true" width="1000" class="zoom"/>

Key findings:

- Overall trend: I typically listen to songs that are up to 10 years old, regardless of the season.
- Summer nostalgia: During summer, I tend to listen to the oldest songs compared to other seasons. This might be because summer free time makes me nostalgic for past experiences.
- Autumn freshness: In autumn, I listen to the newest music or songs I've most recently added to my playlists.
- Winter and spring: These seasons fall in between summer and autumn in terms of how old the music I listen to is.
- Occasional oldies: In all seasons, I sometimes listen to much older songs, going back 60-70 years.
- Preference for older music: Across all seasons, I tend to listen to more older songs than newer ones, but this trend is strongest in summer and weakest in autumn.

This pattern suggests that my mood and the time of year influence my music choices, with summer bringing out my most nostalgic side and autumn inspiring me to explore newer tunes.

### 10. I counted unique genres and did a [Pareto](https://www.cec.health.nsw.gov.au/CEC-Academy/quality-improvement-tools/pareto-charts#:~:text=The%20Pareto%20Chart%20is%20a,represented%20by%20the%20curved%20line.) analysis to see what genres of music make up most of my listening. 
I am unclear on what to glean from this for now, but it was interesting to see that nearly 50% of my music falls into just 30 genres when there are 1412 distinct ones present! The graph below just shows the top 100 genres so you cannot see the Pareto shape/tail very clearly. I realized that if I wanted to do any clustering later on, I would have to delve into this deeper.  

<img src="images/pareto_zoom.png?raw=true" width="1000" class="zoom"/>

### 11. I also wanted to look at total track duration across seasons to see when I listened to longer playlists / more music by season but also by year.

Again, unsurprisingly, I had a lot of free time in the winter and in 2020 during the pandemic.

<img src="images/total_duration_season.png?raw=true" width="1000" class="zoom"/>

<img src="images/duration_over_years.png?raw=true" width="1000" class="zoom"/>


### 12. Finally and what sets the stage up for the next phase of this project, which is sentiment analysis on song lyricsusing LLM's, I made basic word clouds track name for each season to see what the most frequently occurring words were in song titles.

Another reason I wanted to do this was because Spotify already has some sort of sentiment tracking called "Valence"

<img src="images/winter_wordcloud.png?raw=true" width="1000" class="zoom"/>
**Winter**: The winter word cloud highlights significant words like "love," "one," "night," "home," and "Christmas." It reflects winter-specific themes and emotions, balancing positive and negative feelings. Overall, it suggests winter is a mix of both holiday-related songs and introspective tunes about love and life.

<img src="images/spring_wordcloud.png?raw=true" width="1000" class="zoom"/>
**Spring**: The spring word cloud emphasizes words such as "love," "good," "feel," "summer," "new," and "sun." It shows a shift towards positivity and renewal, capturing the upbeat and fresh vibe of the spring season. Songs likely center around themes of new beginnings, happiness, and optimism.

<img src="images/summer_wordcloud.png?raw=true" width="1000" class="zoom"/>
**Summer**: The summer word cloud features words like "summer," "party," "feel," "night," "girl," "life," and "dance." It underscores the season's lively, carefree spirit, with many songs focusing on fun, adventure, and enjoying life to the fullest. The energy and enthusiasm of summer clearly shine through.

<img src="images/autumn_wordcloud.png?raw=true" width="1000" class="zoom"/>
**Autumn**: The fall word cloud highlights words such as "love," "fall," "night," "one," "back," and "heart." Fall seems to reflect a balance of love and introspection, with songs often focusing on themes of romance, reflection, and transition. The season's contemplative nature is mirrored in the music.

---

### Applications of my analysis:

I can see this kind of work being useful in the mental health and wellness space. These were some ideas I had: 

1. **Identify Mood Patterns:** Correlate sentiment in song lyrics with periods of emotional change to understand how music reflects and influences mood.
2. **Enhance Therapy:** Inform music therapy by tailoring music to specific emotional needs, helping with anxiety, depression, or stress.
3. **Explore Seasonal Affective Disorder (SAD):** Examine seasonal patterns in music preferences to understand the impact of seasonal changes on mental health.

---

### With this, I conclude the first phase of my project and hope to delve into the more specific sentiment analysis next! Thanks for taking the time to go through it all, and let me know your thoughts or feedback! 

#### Click here to see the Jupyter Notebook for this EDA!
--- 
