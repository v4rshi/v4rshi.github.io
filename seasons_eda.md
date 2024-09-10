## **Soundtrack of Seasons**: Unraveling My Spotify Saga Over The Last 9 Years

#### Click here to see the Jupyter Notebook for [this EDA](https://github.com/v4rshi/v4rshi.github.io/blob/master/spotify_project_notebooks/seasons_eda.ipynb)!
--- 
**Project Description**: I was able to get playlist data for my Spotify playlists thanks to a website called [Exportify](https://exportify.net/). It made me wonder, can I use this data to understand my mood and well-being over the years based on the season of the year I listened to something and the sentiment of the songs (name and lyrics) themselves?

**Data**: My dataset spans from April 2016 to August 2024. Each entry contains rich metadata including artist, track, addition date, and genre. It also includes an attribute called 'Valence', which captures the sentiment of a song. Tracks with high valence sound more positive (happy, cheerful, euphoric), while tracks with low valence sound more negative (sad, depressed, angry). Read more about it [here](https://community.spotify.com/t5/Spotify-for-Developers/Valence-as-a-measure-of-happiness/td-p/4385221). 

**Motivation & Hypothesis**: This dataset spans a transformative decade of my life, from college in Indiana to married life in San Francisco (and a deadly pandemic in the middle), with Spotify as my constant companion through it all. (Fun Fact: my husband and I even bonded over a Spotify '30 Songs for 30 Days' playlist challenge when we first met!)

My playlists are like musical journals, reflecting my emotions and life events. This project explores how my taste evolved and how playlist traits might correlate with my emotional state. While Spotify's "valence" is cool, I'm aiming for a more nuanced emotional map of my musical journey.

Key focus areas for this project include: 

1. Analyze musical taste evolution over time
2. Examine seasonal patterns in playlists (and see if I am as predictable as I think I am)
3. Perform sentiment analysis using LLM's on song lyrics, focusing on my unemployment period (July 2023-present)

By doing this analysis, I hope to reveal how my music choices reflect my life experiences and emotions. 

##### **Note: Data shows song additions, not play frequency. Play data would enable more in-depth analysis of listening patterns.**


---

<style>
.zoom {
  transition: transform 0.5s ease;
}
.zoom.zoomed {
  transform: scale(2.5);
}
</style>



## Findings and Visualizations: 
### NOTE: Click on any graph to zoom in! 

### 1. The first thing I looked at was who my most listened-to artists were.
I was fully expecting my top artist to be Charli XCX but it is actually... Future??? I did not see this in my Future.

<img src="images/spotify_project/top_20_artists.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

To dig into this deeper, I looked into when I added all the songs with Future on them... to find most of it was this year. 

<img src="images/spotify_project/future_breakdown.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

Bingo! This year, Future became my top artist because 'We Don't Trust You' and 'We Still Don't Trust You,' collaborations with Metro Boomin and Future, were released. I had those albums on repeat, leading me to add many Future songs and collaborations to my playlists.

### 2. This summer was a [BRAT](https://www.cnn.com/2024/07/23/style/brat-summer-green-explained/index.html) summer for me—but who were my most listened-to artists across all seasons in my listening history? *(P.S. Click "BRAT" if you're unfamiliar with the term.)*
It turns out spring is "BRAT green" for Charli XCX! Each season has its own vibe: winter is a bit all over the place, featuring Disney, Britney Spears, and BTS.

<img src="images/spotify_project/top_10_seasonal.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

### 3.I analyzed the number of songs I added to playlists over the years, broken down by month and season, to identify when I was most actively curating my music

I wasn’t surprised to see the erratic nature of my playlist curation until 2022, when I began my first full-time job. With work taking up most of my time, my music curation became less intentional. The spike in August 2024 reflects a period when I relied on music as a coping mechanism during a particularly stressful time.

<img src="images/spotify_project/monthly_adds_by_season.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

### 4. I tried to visualize this differently with number of songs added by season over the years.

It's clear I was most active during the pandemic in 2020 and while unemployed in 2024—both times when I was dealing with a lot in my personal life.

<img src="images/spotify_project/monthly_song_adds_by_season_linechart.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>


### 5. I then explored the volume of songs added across seasons. To visualize this, I normalized the data by dividing the number of songs added each season by the number of days in that season and then by the 9 years in my dataset (almost a third of my life!).

This approach makes sense to me since I was most active in the winter. During college breaks and extreme weather, I spent more time indoors and relied on music to pass the time.

<img src="images/spotify_project/normalized_graph_2.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

### 6. I visualized the seasonal distributions of various music traits, such as Danceability, Valence, Energy, and Tempo, to understand how my music preferences shift throughout the year.

The visual reveals that my taste remains consistent across seasons, with a preference for energetic and danceable songs. Clearly, I love music that sets the mood for a good time!

<img src="images/spotify_project/other_trait_distribution.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

### 7. Next, I analyzed the distributions of songs by season and the year they were added to playlists.

I focused on comparing 2019-2020 and 2023-2024 to see how they differed. My rationale for this comparison is as follows::

- 2020 was the year of the pandemic, and 2019 is a baseline to compare pre and post COVID-19 music preferences
  <img src="images/spotify_project/attributes19.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
  <img src="images/spotify_project/attributes20.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
  
- 2023 was the year I got married but 2024 was the year I was stuck without a job in a bad market
  <img src="images/spotify_project/attributes23.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
  <img src="images/spotify_project/attributes24.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

I broke down each year into seasons to identify any trends, but to avoid cluttering this page with too many graphs, I'll summarize my findings below:

Between 2019 and 2020, my music preferences shifted towards more energetic and positive songs. Despite 2020’s pandemic hardships, it was also the year I was unexpectedly admitted to graduate school. This personal triumph might explain my shift towards upbeat music, highlighting how individual experiences can contrast with broader global events.

From 2023 to 2024, my music preferences dropped in all attributes except tempo. This aligns with the challenges of 2024, especially navigating a tough job market. The decline in most attributes likely mirrors my emotional state, while the higher tempo suggests a need for motivation during stressful times. My playlists reflect my professional struggles and emotions.

---
### 8. I couldn’t overlook analyzing the Valence of songs, even though I plan to conduct my own sentiment analysis in the next step of this project.

Initially, I plotted Valence over time and included a monthly moving average, but the resulting graph was too messy and hard to interpret.
##### Note, the gap in the graph is around the time I briefly used Apple Music - a time we will not speak of again... hehe. 
<img src="images/spotify_project/valence_messy.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

Instead, I plotted a graph to analyze and visualize the average monthly valence of my Spotify playlist data over time, with annotations for significant life events.
<img src="images/spotify_project/valence_life_event.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
Observations:
- Fluctuations in Valence: Sharp drops and spikes in Valence often align with significant life events.
- Notable Drops: Dips in Valence are seen around events like "A Terrible Birthday," "Huge Fight with Someone Close," and "Loved One Died," indicating negative experiences.
- Notable Spikes: Increases in Valence occur around events like "Reconciled with a Friend" and "Got Married," suggesting positive experiences.
- General Trend: Valence remains generally stable but fluctuates with life events.
  
These patterns suggest that my music preferences reflect my emotional state. This insight encourages a deeper exploration using sentiment analysis to understand my emotions during different periods.

### 9. I thought it would be interesting to see how my top 10 genres varied by season. In short, not much changed. 
I was surprised to find 'Modern Rock' appearing in my winter playlists. It turns out that this genre's presence in winter was largely due to additions from 2016, which seems like an anomaly in my usual listening patterns.

<img src="images/spotify_project/top_10_genres_by_season.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

I then tried to visualize this differently with a stacked bar chart and over the top 20 genres overall

<img src="images/spotify_project/top_genres_by_season_barplot.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
This chart displays the popularity of various music genres across seasons:

- Pop is the most popular genre overall, followed by EDM and pop dance.
- Many genres, especially pop and EDM, are more popular in winter.
- Some genres like rap and hip hop show stronger popularity in summer.
- There's a wide range of genres represented, from mainstream to niche.
- Electronic and dance-oriented genres dominate the top rankings.
- All genres show some seasonal variation in popularity.
- Even less popular genres maintain a presence across all seasons, like uk dance and r&b.

I also did this by top 5 Genres over the years separated by season: 
<img src="images/spotify_project/genres_years_stacked.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
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

<img src="images/spotify_project/currentn_v_nostalgic_boxplot.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

Key findings:

- Overall trend: I typically listen to songs that are up to 10 years old, regardless of the season.
- Summer nostalgia: During summer, I tend to listen to the oldest songs compared to other seasons. This might be because summer free time makes me nostalgic for past experiences.
- Autumn freshness: In autumn, I listen to the newest music or songs I've most recently added to my playlists.
- Winter and spring: These seasons fall in between summer and autumn in terms of how old the music I listen to is.
- Occasional oldies: In all seasons, I sometimes listen to much older songs, going back 60-70 years.
- Preference for older music: Across all seasons, I tend to listen to more older songs than newer ones, but this trend is strongest in summer and weakest in autumn.

This pattern suggests that my mood and the time of year influence my music choices, with summer bringing out my most nostalgic side and autumn inspiring me to explore newer tunes.

I also broke it down by year to try and see in greater detail if this trend of listening to nostalgic music held true: 
<img src="images/spotify_project/boxplot_years.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

It is quite clear that the trend of listening to older music on average remains the same, with the exceptions of Spring 2023 and (part) of Winter 2024, where more songs were closer to the year of release than not, indicating a bias to newer releases.

### 11. I counted unique genres and did a [Pareto](https://www.cec.health.nsw.gov.au/CEC-Academy/quality-improvement-tools/pareto-charts#:~:text=The%20Pareto%20Chart%20is%20a,represented%20by%20the%20curved%20line.) analysis to see what genres of music make up most of my listening. 
For those unfamiliar with what a Pareto (also known as the 80/20 rule) suggests 80% of effects come from 20% of causes, helping people prioritize efforts on the most impactful areas. Sometimes it may not even be 80/20, but that is the ratio most commonly used. 

 I am unclear on what to glean from this for now, but it was interesting to see that nearly 50% of my music falls into just 30 genres when there are 1412 distinct ones present! The graph below just shows the top 100 genres so you cannot see the Pareto shape/tail very clearly. I realized that if I wanted to do any clustering later on, I would have to delve into this deeper.  

<img src="images/spotify_project/pareto_zoom.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

### 12. I also wanted to look at total track duration across seasons to see when I listened to longer playlists / more music by season but also by year.

Again, unsurprisingly, I had a lot of free time in the winter across all my data and in the year 2020 during the pandemic because those playlists seem to be looooong. 

<img src="images/spotify_project/total_duration_season.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

<img src="images/spotify_project/duration_over_years.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>


### 13. Finally and what sets the stage up for the next phase of this project, which is sentiment analysis on song lyrics using LLM's, I made basic word clouds track name for each season to see what the most frequently occurring words were in song titles.

I know Spotify tracks the "Valence" of songs, but can I see what my overall mood was by looking at a word cloud of the track titles? After all, a picture is (quite literally) worth a thousand words! 

<img src="images/spotify_project/winter_wordcloud.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
**Winter**: The winter word cloud highlights significant words like "love," "one," "night," "home," and "Christmas." It reflects winter-specific themes and emotions, balancing positive and negative feelings. Overall, it suggests winter is a mix of both holiday-related songs and introspective tunes about love and life.

<img src="images/spotify_project/spring_wordcloud.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
**Spring**: The spring word cloud emphasizes words such as "love," "good," "feel," "summer," "new," and "sun." It shows a shift towards positivity and renewal, capturing the upbeat and fresh vibe of the spring season. Songs likely center around themes of new beginnings, happiness, and optimism.

<img src="images/spotify_project/summer_wordcloud.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
**Summer**: The summer word cloud features words like "summer," "party," "feel," "night," "girl," "life," and "dance." It underscores the season's lively, carefree spirit, with many songs focusing on fun, adventure, and enjoying life to the fullest. The energy and enthusiasm of summer clearly shine through.

<img src="images/spotify_project/autumn_wordcloud.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
**Autumn**: The fall word cloud highlights words such as "love," "fall," "night," "one," "back," and "heart." Fall seems to reflect a balance of love and introspection, with songs often focusing on themes of romance, reflection, and transition. The season's contemplative nature is mirrored in the music.

---

### Applications of my analysis:

I can see this kind of work being useful in the mental health and wellness space. These were some ideas I had: 

1. **Identify Mood Patterns:** Correlate sentiment in song lyrics with periods of emotional change to understand how music reflects and influences mood.
2. **Enhance Therapy:** Inform music therapy by tailoring music to specific emotional needs, helping with anxiety, depression, or stress.
3. **Explore Seasonal Affective Disorder (SAD):** Examine seasonal patterns in music preferences to understand the impact of seasonal changes on mental health.
4. **Seasonally Tailored Playlists**: Spotify could utilize this project to recommend playlists that are tailored to users each season, based on their historical listening data and the preferences of similar users.
5. **Emotion-Based Playlists**: By analyzing a user’s description of their current mood, Spotify could create highly personalized playlists that go beyond the existing "Daylist" feature, providing a more accurate reflection of the user's emotions in real time.

---

Let's examine the ethical data implications for each of these ideas:

1. **Identify Mood Patterns:**
   - Privacy concerns: Tracking users' emotional states over time could be considered invasive.
   - Data security: Emotional data is sensitive and requires robust protection.
   - Consent: Users should be fully informed about how their listening habits are being interpreted.
   - Accuracy: There's a risk of misinterpreting correlations as causation.

2. **Enhance Therapy:**
   - Medical ethics: Using AI-driven recommendations in therapy requires careful consideration and possibly regulation.
   - Liability: Who is responsible if AI-recommended music negatively affects a patient?
   - Confidentiality: Maintaining patient-therapist confidentiality while using third-party services.
   - Informed consent: Patients must understand and agree to the use of AI in their treatment.

3. **Explore Seasonal Affective Disorder (SAD):**
   - Potential for misdiagnosis: Music preferences alone are not sufficient to diagnose mental health conditions.
   - Data bias: Ensuring the dataset represents diverse populations and geographic locations.
   - Cultural sensitivity: Accounting for cultural differences in music preferences and SAD prevalence.

4. **Seasonally Tailored Playlists:**
   - User autonomy: Balancing personalization with user choice and discovery.
   - Transparency: Clearly communicating how and why certain music is recommended.
   - Data retention: Determining how long historical data should be kept and used.
   - Opt-out options: Allowing users to decline this feature without losing core service functionality.

5. **Emotion-Based Playlists:**
   - Emotional manipulation: Potential for influencing users' moods, which raises ethical questions.
   - Data collection: Gathering real-time emotional data requires clear user consent and robust data protection.
   - Accuracy and reliability: Ensuring the system can accurately interpret emotional states from user input.
   - Potential for misuse: Safeguarding against exploitation of users' emotional vulnerabilities.

General ethical considerations across all applications:

1. Data minimization: Collecting only necessary data to provide the service.
2. Transparency: Clearly communicating to users how their data is being used.
3. User control: Providing options for users to manage their data and preferences.
4. Algorithmic bias: Ensuring the AI doesn't perpetuate or exacerbate existing biases.
5. Accessibility: Making sure these features are available and beneficial to diverse user groups.
6. Continuous ethical review: Regularly assessing the impact and implications of these applications.
7. Collaboration with experts: Involving mental health professionals in the development and implementation of these features.

These applications have significant potential benefits, but they also come with substantial ethical responsibilities. Careful consideration, ongoing evaluation, and robust safeguards are necessary to ensure that the technology is used in a way that truly benefits users' mental health and well-being while respecting their privacy and autonomy.

---

### With this, I conclude the first phase of my project and hope to delve into the more specific sentiment analysis on song lyrics next! 

Thanks for taking the time to go through it all, and let me know your thoughts or feedback by emailing me at v4rshi.srini@gmail.com! 

--- 
<script>
document.addEventListener('DOMContentLoaded', function() {
  document.querySelectorAll('.zoom').forEach(function(element) {
    element.addEventListener('click', function() {
      this.classList.toggle('zoomed');
    });
  });
});
</script>
