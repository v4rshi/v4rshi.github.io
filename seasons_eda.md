## **Soundtrack of Seasons**: Unraveling My Spotify Saga Over The Last 9 Years

#### Click here to see the Jupyter Notebook for [this EDA](https://github.com/v4rshi/v4rshi.github.io/blob/master/spotify_project_notebooks/seasons_eda.ipynb)!
--- 
**Project Description**: I was able to get playlist data for my Spotify playlists thanks to a website called [Exportify](https://exportify.net/). It made me wonder, can I use this data to understand my mood and well-being over the years based on the season of the year I listened to something and the sentiment of the songs (name and lyrics) themselves?

**Data**: My dataset spans from April 2016 to August 2024. Each entry contains rich metadata including artist, track, addition date, and genre. It also includes an attribute called 'Valence', which captures the sentiment of a song. Tracks with high valence sound more positive (happy, cheerful, euphoric), while tracks with low valence sound more negative (sad, depressed, angry). Read more about it [here](https://community.spotify.com/t5/Spotify-for-Developers/Valence-as-a-measure-of-happiness/td-p/4385221). 

**Motivation & Hypothesis**: This dataset captures a transformative period in my life. From relocating from Dubai to Indiana for college, navigating the global pandemic (and graduate school in lockdown), experiencing personal losses, moving to San Francisco, starting my career, meeting my now husband and getting married, and transitioning between jobs. Throughout these experiences, Spotify remained a constant companion. (Also fun fact, my husband and I bonded over Spotify when we first started talking too!)

I've observed that my playlists often serve as a form of musical journaling, reflecting my emotional state and circumstances. This project aims to analyze the evolution of my musical preferences over time and explore potential correlations between playlist characteristics (content, length, addition frequency) and my emotional state at the time. Valence is a cool attribute, but I think I want more nuance than a number - I want a clearly defined set of emotions associated with my musical history. 

Key focus areas for this project include: 

1. Temporal analysis of musical taste to confirm if the data reveals what I think know (or do not know) about my musical taste 
2. Seasonal patterns in playlist composition, particularly relative to seasons and whatever weather changes they bring
3. Sentiment analysis of song lyrics using LLM's, with a specific focus on the period of July 2023 to now (coinciding with my period of unemployment)

By examining these data points, I hope to uncover insights into how my music choices have mirrored my life experiences and emotional states during this pivotal time. 

##### **It is important to note that this data did not include how often I listened to specific songs, just when I added them to a given playlist. This data would be great for a more in-depth analysis of my listening patterns.**

---

<style>
  .zoom-container {
    position: relative;
    display: inline-block;
  }

  .zoom-container::after {
    content: "Click to Zoom";
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: rgba(0, 0, 0, 0.7);
    color: white;
    padding: 5px 10px;
    border-radius: 5px;
    opacity: 0;
    transition: opacity 0.3s ease;
  }

  .zoom-container:hover::after {
    opacity: 1;
  }

  .zoom {
    transition: transform 0.3s ease;
  }

  .zoom.zoomed {
    transform: scale(3);
  }
</style>

<script>
document.querySelectorAll('.zoom-container').forEach(container => {
  const img = container.querySelector('.zoom');
  let zoomed = false;

  container.addEventListener('click', () => {
    zoomed = !zoomed;
    img.classList.toggle('zoomed', zoomed);
  });
});
</script>

## Findings and Visualizations: 
### NOTE: Click on all graphs to see a bigger version of them! 

### 1. The first thing I looked at was who my most listened to artists were.
I was fully expecting my top artist to be Charli XCX but in a rather surprising turn of events, its Future??? I did not see this in my Future, that is for sure.

<div class="zoom-container">
  <img src="images/spotify_project/top_20_artists.png?raw=true" width="1000" class="zoom"/>
</div>

To dig into this deeper, I looked into when I added all the songs with Future on them... to find most of it was this year. 

<div class="zoom-container">
  <img src="images/spotify_project/future_breakdown.png?raw=true" width="1000" class="zoom"/>
</div>

Bingo! This year, Future became my top artist because 'We Don't Trust You' and 'We Still Don't Trust You,' collaborations with Metro Boomin and Future, were released. My husband and I had those albums on repeat, leading me to add many Future songs and collaborations to my playlists.

### 2. This summer is a BRAT summer for me - but historically was that always the case across my entire listening history?
Looks like spring is BRAT green! Each season is quite different, winter seemingly being all over the place since Disney, Britney Spears and BTS are all on there! 

<div class="zoom-container">
  <img src="images/spotify_project/top_10_seasonal.png?raw=true" width="1000" class="zoom"/>
</div>

### 3. I chose to look at add number of songs over the years (by month and season) to see when I most actively added music to playlists

I wasn't surprised to see the erratic nature of my playlist curation until 2022, when I started my first full-time job. With work consuming most of my time, I wasn't curating my music as intentionally. The spike in August 2024 can be attributed to using music as a coping mechanism during a particularly stressful period.

<div class="zoom-container">
  <img src="images/spotify_project/monthly_adds_by_season.png?raw=true" width="1000" class="zoom"/>
</div>

### 4. I tried to visualize this differently with number of songs added by season over the years.

It is clear that the pandemic in 2020 and my time being unemployed in 2024 are when I am most active. This coincides with when I was going through a lot in my personal life, too. 

<div class="zoom-container">
  <img src="images/spotify_project/monthly_song_adds_by_season_linechart.png?raw=true" width="1000" class="zoom"/>
</div>

### 5. I wanted to then look at song-adding volume over the seasons. I tried to visualize this differently where I normalized my data by dividing each season by no. days in a season and then dividing that by the number of years in my dataset (9 Years! Almost a third of my life!). 

This makes sense to me because I was generally most active in the winter. During college breaks and extreme weather, when I spent more time indoors, I relied on music more to pass the time.

<div class="zoom-container">
  <img src="images/spotify_project/normalized_graph_2.png?raw=true" width="1000" class="zoom"/>
</div>

### 6. I tried visualizing seasonal distributions for various other music traits, like Danceability, Valence, Energy and Tempo, to get a general sense of what kind of music I liked in different seasons. 

This visual shows that my taste remains consistent across seasons, favoring songs that are energetic and danceable. Ya girl like music she can have a good time to! 

<div class="zoom-container">
  <img src="images/spotify_project/other_trait_distribution.png?raw=true" width="1000" class="zoom"/>
</div>

### 7. I wanted to then look at the distributions by season and year it was added to a playlist.

I chose to pay the closest attention to 2019-2020, 2023-2024 and see how they compared to one another. The rationale is as follows:

- 2020 was the year of the pandemic, and 2019 is a baseline to compare pre and post COVID-19 music preferences
  <div class="zoom-container">
    <img src="images/spotify_project/attributes19.png?raw=true" width="1000" class="zoom"/>
  </div>
  <div class="zoom-container">
    <img src="images/spotify_project/attributes20.png?raw=true" width="1000" class="zoom"/>
  </div>
  
- 2023 was the year I got married but 2024 was the year I was stuck without a job in a bad market
  <div class="zoom-container">
    <img src="images/spotify_project/attributes23.png?raw=true" width="1000" class="zoom"/>
  </div>
  <div class="zoom-container">
    <img src="images/spotify_project/attributes24.png?raw=true" width="1000" class="zoom"/>
  </div>

I did also break each year down into seasons to see any seasonal trends, but to not clutter this page with too many graphs I will summarize my observations below:

The shift in my music preferences between **2019 and 2020** shows a surprising trend towards, on average, more energetic and positive songs. While 2020 is often associated with the hardships of the COVID-19 pandemic, it was also the year I was unexpectedly admitted to graduate school. This personal triumph, especially significant given the closed borders and uncertainty, may explain my gravitation towards upbeat music. My experience highlights how individual circumstances can contrast with broader narratives during global events. 

Between **2023 and 2024**, my music preferences show a drop, on average, in all attributes except tempo. This shift aligns with the challenges I'm facing in 2024, particularly navigating a difficult job market. The decrease in most musical attributes likely reflects my current emotional state, while the increased tempo might indicate a need for motivation or energy during these stressful times. My playlist has essentially become a reflection of my professional struggles and associated emotions. 

Note to self: Either make these playlists private or start a new career as the world's most reluctant psychic. "For just $9.99, I'll predict your future by analyzing your 'Most Played' list!" Hmm, maybe I'm onto something here...

---
### 8. I would be remiss to not look into Valence of songs, even though I want to do my own version of sentiment analysis in the next step of this project. 

Initially, I plotted valence over time as well as a monthly moving average to find that this graph was messy and impossible to interpret. 
<div class="zoom-container">
  <img src="images/spotify_project/valence_messy.png?raw=true" width="1000" class="zoom"/>
</div>

Instead, I plotted a graph to analyze and visualize the average monthly valence of my Spotify playlist data over time, with annotations for significant life events.
<div class="zoom-container">
  <img src="images/spotify_project/valence_life_event.png?raw=true" width="1000" class="zoom"/>
</div>
Observations:
- Fluctuations in Valence: There are several sharp drops and spikes in valence, often coinciding with life events.
- Notable Drops: Significant dips in valence appear around "A Terrible Birthday," "Huge Fight with Someone Close," and "Loved One Died," suggesting these were negative experiences.
- Notable Spikes: Increases in valence are observed around events like "Reconciled with a Friend" and "Got Married," indicating these were positive experiences.
- General Trend: The valence seems to be somewhat stable but with recurrent fluctuations corresponding to life events.
- 
My music preferences clearly mirror my emotional state, suggesting a detailed sentiment analysis of song lyrics could yield fascinating insights into my specific emotions during different periods. This validation encourages a deeper exploration using sentiment analysis techniques!

### 9. I thought it would be interesting to see what my top 10 genres were by season and if they varied at all.
 In short, barely. I still am basic as hell and listen to a lot of pop, however the genres following that moved around but were only edm, hip hop, rap and/or some pop variation. What was surprising to me was the random appearance of 'Modern Rock' in the Wintertime. Wintertime House of Blues, I guess?

<div class="zoom-container">
  <img src="images/spotify_project/top_10_genres_by_season.png?raw=true" width="1000" class="zoom"/>
</div>

I then tried to visualize this differently with a stacked bar chart and over the top 20 genres overall

<div class="zoom-container">
  <img src="images/spotify_project/top_genres_by_season_barplot.png?raw=true" width="1000" class="zoom"/>
</div>
This chart displays the popularity of various music genres across seasons:

- Pop is the most popular genre overall, followed by EDM and pop dance.
- Many genres, especially pop and EDM, are more popular in winter.
- Some genres like rap and hip hop show stronger popularity in summer.
- There's a wide range of genres represented, from mainstream to niche.
- Electronic and dance-oriented genres dominate the top rankings.
- All genres show some seasonal variation in popularity.
- Even less popular genres maintain a presence across all seasons, like uk dance and r&b.

I also did this by top 5 Genres over the years separated by season: 
<div class="zoom-container">
  <img src="images/spotify_project/genres_years_stacked.png?raw=true" width="1000" class="zoom"/>
</div>
Key points:

- Wide variety of genres represented
- Genre popularity fluctuates seasonally and yearly
- Some genres (e.g., pop, rap) appear consistently
- Summer 2017 shows highest genre diversity
- Recent years (2022-2024) have more stable genre distribution
- New genres emerge over time
- Data shown as percentages for easy comparison
- Covers 8 years, good for long-term trend analysis

### 10. I wondered, do I like current releases or nostalgic music more, and does this vary by season?
The boxplot graph below shows how my music listening habits change throughout the year. It compares the age of songs I listen to (how long ago they were released compared to when it was added to a playlist) across different seasons. The insights were very interesting. 

A primer on what a boxplot even is: it is a simple visual tool that shows the spread and symmetry of a dataset by dividing it into quartiles and highlighting key statistics like the median and potential outliers. It uses a box to represent the middle 50% of the data and lines extending from the box to show the range, making it easy to see how data is distributed. Feel free to also refer to [this guide](https://www.simplypsychology.org/boxplots.html) on how to interpret boxplots.

<div class="zoom-container">
  <img src="images/spotify_project/currentn_v_nostalgic_boxplot.png?raw=true" width="1000" class="zoom"/>
</div>

Key findings:

- Overall trend: I typically listen to songs that are up to 10 years old, regardless of the season.
- Summer nostalgia: During summer, I tend to listen to the oldest songs compared to other seasons. This might be because summer free time makes me nostalgic for past experiences.
- Autumn freshness: In autumn, I listen to the newest music or songs I've most recently added to my playlists.
- Winter and spring: These seasons fall in between summer and autumn in terms of how old the music I listen to is.
- Occasional oldies: In all seasons, I sometimes listen to much older songs, going back 60-70 years.
- Preference for older music: Across all seasons, I tend to listen to more older songs than newer ones, but this trend is strongest in summer and weakest in autumn.

This pattern suggests that my mood and the time of year influence my music choices, with summer bringing out my most nostalgic side and autumn inspiring me to explore newer tunes.

I also broke it down by year to try and see in greater detail if this trend of listening to nostalgic music held true: 
<div class="zoom-container">
