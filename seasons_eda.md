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

Between **2019 and 2020**, my music preferences shifted towards more energetic and positive songs. Despite 2020’s pandemic hardships, it was also the year I was unexpectedly admitted to graduate school. This personal triumph might explain my shift towards upbeat music, highlighting how individual experiences can contrast with broader global events.

From **2023 to 2024**, my music preferences dropped in all attributes except tempo. This aligns with the challenges of 2024, especially navigating a tough job market. The decline in most attributes likely mirrors my emotional state, while the higher tempo suggests a need for motivation during stressful times. My playlists reflect my professional struggles and emotions.

---
### 8. I couldn’t overlook analyzing the Valence of songs, even though I plan to conduct my own sentiment analysis in the next step of this project.

Initially, I plotted Valence over time and included a monthly moving average, but the resulting graph was too messy and hard to interpret.
##### Note, the gap in the graph is around the time I briefly used Apple Music - a time we will not speak of again... hehe. 
<img src="images/spotify_project/valence_messy.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

Instead, I plotted a graph to analyze and visualize the average monthly valence of my Spotify playlist data over time, with annotations for significant life events.
<img src="images/spotify_project/valence_life_event.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
Observations:
- **Fluctuations in Valence**: Sharp drops and spikes in Valence often align with significant life events.
- **Notable Drop**s: Dips in Valence are seen around events like "A Terrible Birthday," "Huge Fight with Someone Close," and "Loved One Died," indicating negative experiences.
- **Notable Spikes**: Increases in Valence occur around events like "Reconciled with a Friend" and "Got Married," suggesting positive experiences.
- **General Trend**: Valence remains generally stable but fluctuates with life events.
  
These patterns suggest that my music preferences reflect my emotional state. This insight encourages a deeper exploration using sentiment analysis to understand my emotions during different periods.

### 9. I thought it would be interesting to see how my top 10 genres varied by season. In short, not much changed. 
I was surprised to find 'Modern Rock' appearing in my winter playlists. It turns out that this genre's presence in winter was largely due to additions from 2016, which seems like an anomaly in my usual listening patterns.

<!---img src="images/spotify_project/top_10_genres_by_season.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/-->
<iframe src="images/spotify_project/top_10_genres_by_season.html" width="500" height="300"></iframe>

I was then curious to see which years' wintertime this rock music phase happened in

<iframe src="images/spotify_project/rock_winter.html" width="500" height="300"></iframe>

It is pretty apparent that as time passed, this genre no longer appeared in my playlists, appearing as little as 1 time in 2023 (talk about ROCK bottom :P)

I then tried to visualize this differently with a stacked bar chart and over the top 20 genres overall

<!img src="images/spotify_project/top_genres_by_season_barplot.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>
This chart displays the popularity of various music genres across seasons:

- Pop leads in overall popularity, followed by EDM and pop dance.
- Pop and EDM are particularly popular in winter.
- Rap and hip hop gain traction in summer.
- Genres range from mainstream to niche, with electronic and dance genres topping the list.
- All genres exhibit seasonal popularity shifts, including less popular ones like UK dance and R&B.

I also did this by top 5 Genres over the years separated by season: 
<iframe src="images/spotify_project/top5genre_chart.html" width="500" height="300"></iframe>
Key points:

- Genres vary widely and shift seasonally and yearly.
- Pop and rap appear consistently.
- Summer 2017 had the most diverse genre representation.
- Recent years (2022-2024) show more stable genre distribution.
- New genres emerge over time.

### 10. I explored whether I prefer current or nostalgic music and if this changes by season. The boxplot below shows how the age of songs I listen to varies across seasons, revealing some interesting patterns.

A boxplot visually represents data spread and symmetry by dividing it into quartiles, showing the median and potential outliers. For more on interpreting boxplots, see [this guide](https://www.simplypsychology.org/boxplots.html).

<img src="images/spotify_project/currentn_v_nostalgic_boxplot.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

**Key findings:**

- **Overall:** I usually listen to songs up to 10 years old, no matter the season.
- **Summer:** I dive into the oldest tracks, probably because summer nostalgia kicks in.
- **Autumn:** I prefer the freshest tunes or the ones I've recently added to my playlists.
- **Winter and Spring:** My music choices are a mix of summer's oldies and autumn's new hits.
- **Occasional Oldies:** I throw in some tracks from 60-70 years ago every now and then.
- **Older Music Preference:** I lean towards older songs year-round, especially in summer and least in autumn.

In summary, my mood and the season shape my music preferences, with summer making me nostalgic and autumn getting me excited about new tunes.

I also looked at yearly trends to see if this nostalgic streak holds up over time:
<img src="images/spotify_project/boxplot_years.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

The trend of favoring older music remains consistent, except for Spring 2023 and part of Winter 2024, when I leaned towards newer releases.

### 11. I counted unique genres and did a [Pareto](https://www.cec.health.nsw.gov.au/CEC-Academy/quality-improvement-tools/pareto-charts#:~:text=The%20Pareto%20Chart%20is%20a,represented%20by%20the%20curved%20line.) analysis to see what genres of music make up most of my listening. 
For those unfamiliar with what a Pareto (also known as the 80/20 rule) suggests 80% of effects come from 20% of causes, helping people prioritize efforts on the most impactful areas. Sometimes it may not even be 80/20, but that is the ratio most commonly used. 

The fact that nearly 50% of my music falls into just 30 genres out of 1412 suggests a concentration of preference. Although the graph below shows only the top 100 genres, making the Pareto distribution less visible, this finding suggests a need for deeper exploration of the genres present in the dataset. I will hold off on this for now, but I can see this being interesting if I wanted to eventually build a recommendation engine.  

<img src="images/spotify_project/pareto_zoom.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

### 12. I created t-SNE Visualization and Analysis of Music Clustering Based on Audio Features
For those unfamiliar, t-SNE is a technique that simplifies complex, high-dimensional data into a 2D map to reveal patterns, while KMeans groups similar items into clusters (and click here to learn about [t-SNE](https://towardsdatascience.com/t-sne-clearly-explained-d84c537f53a) and [K-means clustering](https://medium.com/@amit25173/k-means-clustering-for-dummies-a-beginners-guide-399fb8c427fd)). In this analysis, t-SNE helps us visualize the data, and KMeans identifies clusters of songs based on their audio features. Essentially, I’m using these methods to group songs that share similar characteristics from the dataset. It’s an intriguing way to uncover patterns in music! I used the elbow method ([click here to know more about that](https://www.analyticsvidhya.com/blog/2021/01/in-depth-intuition-of-k-means-clustering-algorithm-in-machine-learning/)) to figure out how many clusters was best (turns out to be 4) and this was the outcome:

<iframe src="images/spotify_project/tsne_clustering.html" width="800" height="600"></iframe>

This graph shows a t-SNE (t-Distributed Stochastic Neighbor Embedding) visualization of song clustering based on audio features. Key takeaways are:

1. Number of Clusters:
   The graph and centroid table both indicate 4 distinct clusters (0, 1, 2, 3), represented by different colors in the plot.

2. Cluster Distribution:
   - The clusters appear to have some overlap, which is common in music data due to similarities across genres.
   - There are some clear areas of concentration for each cluster, suggesting that the algorithm has identified meaningful groupings.

3. Cluster Characteristics (based on centroids):
   - Cluster 0 (Purple): Mid-range energy, high danceability, high speechiness. 
   - Cluster 1 (Orange): Highest energy and valence, low speechiness. Likely upbeat, danceable pop.
   - Cluster 2 (Blue): Lowest energy, highest acousticness and instrumentalness. 
   - Cluster 3 (Pink): Second-highest energy, longest duration, lowest popularity. 

4. Spatial Distribution:
   - The clusters are not perfectly separated, indicating some songs share characteristics across clusters.
   - There's a notable spread in each cluster, showing variability within genres or styles.

5. Feature Importance:
   - Energy seems to be a key differentiator, with clear separation between high-energy (Cluster 1) and low-energy (Cluster 2) songs.
   - Acousticness and instrumentalness appear to strongly influence Cluster 2's separation.

6. Popularity:
   - Interestingly, the most popular cluster on average (Cluster 1) is not the most prominent in the visualization, suggesting popularity isn't the primary factor in this clustering.

7. Tempo and Duration:
   - While not directly visible in the t-SNE plot, the centroids show variations in tempo and duration across clusters, contributing to the overall differentiation.

8. Outliers:
   - There are some points scattered away from the main cluster concentrations, possibly representing unique or genre-blending tracks.

In conclusion, this t-SNE visualization effectively represents the complex audio feature space in a 2D format, revealing meaningful clusters that likely correspond to different musical styles or genres. The overlap between clusters reflects the nuanced nature of music categorization, where songs can share characteristics across traditional genre boundaries.

**I also looked at the seasonal distribution of clusters for a kick**

<iframe src="images/spotify_project/cluster_distribution_by_season.html" width="500" height="300"></iframe>

These are my key takeaways: 
1. Seasonal Patterns:
   - Cluster 1 (red) dominates across all seasons, with the highest number of tracks.
   - Cluster 3 (purple) is the second most prevalent, especially in Winter and Autumn.
   - Clusters 0 (blue) and 2 (green) have lower, relatively consistent numbers across seasons.
2. Seasonal Variations:
   - Winter has the highest overall number of tracks across all clusters.
   - Spring shows the lowest overall number of tracks.
   - Summer and Autumn have similar total track counts, falling between Winter and Spring.
3. Cluster Trends:
   - Cluster 1 peaks in Winter, with its lowest point in Spring.
   - Cluster 3 is most prominent in Winter and Autumn, less so in Spring and Summer.
   - Clusters 0 and 2 show less dramatic seasonal fluctuations.

This seasonal analysis complements the t-SNE clustering by showing how music preferences or releases vary throughout the year. It could be valuable for playlist curation, release scheduling, and understanding seasonal music consumption patterns. Music streaming services could use this data to tailor recommendations based on the time of year, while artists and labels might consider optimal release times for different types of music.

### 13. I also wanted to look at total track duration across seasons to see when I listened to longer playlists / more music by season but also by year.

Again, unsurprisingly, I had a lot of free time in the winter across all my data and in the year 2020 during the pandemic because those playlists seem to be looooong. 

<img src="images/spotify_project/total_duration_season.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

<img src="images/spotify_project/duration_over_years.png?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>


### 14. Finally and what sets the stage up for the next phase of this project, which is sentiment analysis on song lyrics using LLM's, I made basic word clouds track name for each season to see what the most frequently occurring words were in song titles.

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

### Applications of My Analysis:

This work could greatly impact mental health and wellness through:

1. **Mood Patterns:** Correlate song lyrics with emotional changes to understand how music influences mood.
2. **Enhanced Therapy:** Tailor music therapy to address anxiety, depression, or stress.
3. **Seasonal Affective Disorder (SAD):** Investigate seasonal music preferences to explore their effect on mental health.
4. **Seasonal Playlists:** Spotify could create playlists based on users’ seasonal listening patterns.
5. **Emotion-Based Playlists:** Develop real-time playlists reflecting users’ current moods.

---

**Ethical Considerations:**

1. **Mood Patterns:**
   - **Privacy:** Tracking emotional states can be intrusive.
   - **Data Security:** Emotional data needs strong protection.
   - **Consent:** Users must know how their data is used.
   - **Accuracy:** Avoid misinterpreting correlations.

2. **Enhanced Therapy:**
   - **Medical Ethics:** Use of AI in therapy should be regulated.
   - **Liability:** Address potential negative impacts of AI recommendations.
   - **Confidentiality:** Maintain privacy between patient and therapist.
   - **Consent:** Patients should agree to AI’s role in their treatment.

3. **SAD:**
   - **Misdiagnosis:** Music preferences alone can’t diagnose mental health issues.
   - **Data Bias:** Ensure data represents diverse populations.
   - **Cultural Sensitivity:** Consider cultural differences in music preferences.

4. **Seasonal Playlists:**
   - **User Autonomy:** Balance personalization with user choice.
   - **Transparency:** Clearly communicate recommendation methods.
   - **Data Retention:** Decide how long to keep user data.
   - **Opt-Out:** Allow users to decline without losing essential features.

5. **Emotion-Based Playlists:**
   - **Emotional Manipulation:** Be cautious about influencing users’ moods.
   - **Data Collection:** Securely gather real-time emotional data with consent.
   - **Accuracy:** Ensure the system correctly interprets moods.
   - **Misuse:** Prevent exploitation of users’ emotional states.

**General Ethical Principles:**

1. **Data Minimization:** Collect only necessary information.
2. **Transparency:** Clearly explain data use.
3. **User Control:** Let users manage their data and preferences.
4. **Algorithmic Bias:** Avoid reinforcing biases.
5. **Accessibility:** Ensure features are inclusive.
6. **Continuous Review:** Regularly evaluate ethical impacts.
7. **Expert Collaboration:** Work with mental health professionals to guide development.

These applications hold promise but require careful ethical consideration to balance benefits with privacy and well-being.

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
