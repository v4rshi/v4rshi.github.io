<link href='https://fonts.googleapis.com/css?family=Bungee' rel='stylesheet'>
<h2 style="font-family: 'Bungee', sans-serif; color: #00d0e3; font-size: 24px;">Sentiment Analysis on Spotify Data and Recommendation System</h2>

### Project Overview
This project aims to perform sentiment analysis on Spotify data to build a dynamic recommendation system. By analyzing the emotional qualities of music, the project seeks to enhance personalized listening experiences and provide insights into user preferences.

I am still working on populating this page and ironing out some kinks, but in the meantime click on the link below to explore my prototype Musical Mood Ring! Select a 'Sentiment' to discover songs with similar vibes!


<nav style="text-align: center;">
  <div style="display: inline-block; background-color: #ffe6f5; border-radius: 25px; padding: 10px 20px; box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);">
    <a href="mood_ring.html" style="font-family: 'Bagel Fat One', sans-serif; font-size: 24px; background: linear-gradient(90deg, #ff6666, #ffb366, #66ff66, #33ccff, #6699ff, #cc99ff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; text-decoration: none;">
      V's Musical Mood Ring
    </a>
  </div>
</nav>
<br> <b4\r>

#THE BELOW IS A WORK IN PROGRESS!!


### The Data
**Timeframe**: April 2016 - August 2024 

**Attributes**: Musical history data, including track names, artists, genres, tempo, release date, lyrics, and sentiment scores

### Motivation & Hypothesis: 
Understanding the emotional impact of music is essential in today’s music landscape. This analysis aims to uncover how sentiment influences music preferences and listener engagement, ultimately leading to a more personalized recommendation system.

## Key Focus Areas

### Data Ingestion
- Process of gathering musical history data from Spotify.
- Steps taken to remove duplicate songs.
- Tools and libraries utilized for data ingestion.

### Lyrics Fetching
- Utilizing the Genius API to fetch lyrics based on track names and artists.
- Discussion of challenges faced, such as API rate limits and slow response times.

### Data Cleaning
- Cleaning lyrics using regex patterns.
- Rationale behind chosen formatting with examples of raw vs. cleaned lyrics.

### Data Storage
- Format of the saved data (CSV) and its structure (columns, data types).
- Importance of organized data for subsequent analysis.

### Sentiment Analysis
- Implementing a pre-trained model from Hugging Face to run sentiment analysis using PyTorch.
- Explanation of the results obtained from the analysis.

### Recommendation System
- Building a dynamic recommendation system using sentiment as a feature.
- How user-selected sentiment leads to song recommendations and overview of the algorithm used to generate new recommendations.

### Interactive HTML Page
- Creating a user-friendly HTML page where users can select an emotion.
- Overview of the HTML page functionality and how users can interact with it.
- Features of the carousel displaying songs, album art, previews, and links to Spotify based on historical data.

### UX Considerations for Carousel Design:
- Ensuring intuitive navigation and accessibility for all users.
- Designing an engaging and visually appealing layout to enhance user interaction.
- Providing clear feedback on user actions, such as song selection and emotional response.
I am still working out the kinks, but in the mean-time, I developed a mood-based recommendation system prototype - check it out! 


-
## Next Steps
- Discuss potential future improvements and extensions to the project, such as enhancing the recommendation algorithm or refining the user interface.

### Applications of the Analysis
- Explore how sentiment analysis can enhance user experience on music platforms through personalized recommendations.

### Ethical Considerations
- Highlight any ethical concerns related to data privacy and the implications of using sentiment analysis in recommendations.

### Feedback
- We welcome your thoughts and feedback! Feel free to reach out with questions or comments.

### References
*coming soon*
<link href='https://fonts.googleapis.com/css?family=Bagel Fat One' rel='stylesheet'>











<style>
  nav a:hover {
    color: #00ff00; /* Brighter green */
  }
</style>

<link href='https://fonts.googleapis.com/css?family=Bungee Shade' rel='stylesheet'>


<br>

<style>
  .floating-button {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background-color: transparent;
    border: none;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .floating-button:hover {
    background-color: rgba(255, 20, 147, 0.1); /* Light hover effect */
  }

  .tooltip {
    visibility: hidden;
    width: 120px;
    background-color: black;
    color: #fff;
    text-align: center;
    border-radius: 5px;
    padding: 5px 0;
    position: absolute;
    z-index: 1;
    bottom: 30px;
    right: 50%;
    margin-right: -60px;
  }

  .floating-button:hover .tooltip {
    visibility: visible;
  }
</style>

<button class="floating-button" onclick="window.location.href='https://v4rshi.github.io/'">
    <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 24 24" fill="hotpink">
        <path d="M12 3l10 9h-3v8h-4v-5h-6v5H5v-8H2l10-9z"/>
    </svg>
    <span class="tooltip">Return To Homepage</span>
</button>

<p style="font-size:9px"> © Copyright of Varshini Srinivas </p>
