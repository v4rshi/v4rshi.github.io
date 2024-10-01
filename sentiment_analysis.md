<link href='https://fonts.googleapis.com/css?family=Bungee' rel='stylesheet'>
<h2 style="font-family: 'Bungee', sans-serif; color: #00d0e3; font-size: 24px;">Sentiment Analysis on Spotify Data and Recommendation System</h2>

### Project Overview
This project aims to perform sentiment analysis on Spotify data to build a personalized recommendation system. By analyzing the emotional qualities of music, the project seeks to enhance personalized listening experiences and provide insights into user preferences.

I am still working on populating this page and ironing out some kinks, but in the meantime click on the link below to explore my prototype Musical Mood Ring! Select a 'Sentiment' to discover songs with similar vibes!


<nav style="text-align: center;">
  <div style="display: inline-block; background-color: #ffe6f5; border-radius: 25px; padding: 10px 20px; box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);">
    <a href="mood_ring.html" style="font-family: 'Bagel Fat One', sans-serif; font-size: 24px; background: linear-gradient(90deg, #ff6666, #ffb366, #66ff66, #33ccff, #6699ff, #cc99ff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; text-decoration: none;">
      V's Musical Mood Ring
    </a>
  </div>
</nav>
<br> <br>

# THE BELOW IS A WORK IN PROGRESS!!


### The Data
**Timeframe**: April 2016 - August 2024 

**Attributes**: Musical history data, including track names, artists, genres, tempo, release date, lyrics, and sentiment scores

### Motivation & Hypothesis: 
Understanding the emotional impact of music is essential in today’s music landscape. This analysis aims to uncover how sentiment influences music preferences and listener engagement, ultimately leading to a more personalized recommendation system.

## Key Focus Areas

### Data Ingestion
- **Overview**: Gathered historical musical data from Spotify using the Spotify API.
- **Steps Taken**: 
  - Collected personal listening history, including track metadata (name, artist, album, duration).
  - Filtered and removed duplicate songs to ensure data integrity.
- **Tools Used**: 
  - **Libraries**: `spotipy` (for Spotify API interaction), `pandas` (for data manipulation), and `numpy` (for numerical operations).
  - **Method**: Deduplication was handled using pandas' `drop_duplicates()` method.

### Lyrics Fetching
- **Approach**: Fetched song lyrics via the Genius API by matching track names and artist information.
- **Challenges**:
  - Faced API rate limits, which required batching requests.
  - Some API responses were slow or incomplete, leading to missing lyrics.

### Data Cleaning
- **Method**: Used regular expressions (regex) to clean up the fetched lyrics, removing unwanted characters and formatting anomalies (e.g., brackets, newlines, special symbols).
- **Example**:
  - **Raw**: "[Verse 1] I’m walking on sunshine! (Yeah, yeah)"
  - **Cleaned**: "I'm walking on sunshine"
- This cleaning process was essential to prepare the lyrics for sentiment analysis.

### Data Storage
- **Format**: Data was stored in CSV files with the following columns:
  - Track Name (string)
  - Artist (string)
  - Album (string)
  - Duration (int)
  - Lyrics (string)
  - Sentiment (string)
- **Importance**: Organized, structured data allowed for seamless integration with machine learning models and simplified future analysis.

### Sentiment Analysis
- **Implementation**: Utilized a pre-trained transformer model from Hugging Face (like `distilbert-base-uncased`) with PyTorch for sentiment analysis.
- **Results**: Classified song lyrics into sentiment categories (positive, negative, neutral), forming the basis for the mood-based recommendation system.

### Recommendation System
- **Concept**: Built a dynamic recommendation engine where users pick a mood, and the system recommends songs based on historical sentiment analysis of lyrics.
- **Algorithm**: Employed a combination of collaborative filtering and sentiment-based recommendations, factoring in user preferences and the emotional tone of songs.

### Interactive HTML Page
- **Design**: 
  - Created an intuitive HTML page where users can select an emotion from a list.
  - Users are presented with a carousel of song recommendations featuring album art, a preview of the song, and links to listen on Spotify.
- **Functionality**: 
  - The page dynamically generates recommendations based on user sentiment input, enhancing the user experience with personalized music choices.

### UX Considerations for Carousel Design
- Focused on intuitive navigation and accessibility.
- Ensured a visually appealing, engaging layout for users.
- Provided clear feedback when users select an emotion or interact with the carousel.

**Prototype Available**: Check out the mood-based recommendation system prototype [here]!

---

### Next Steps
- **Improvements**:
  - Fine-tune the recommendation algorithm for better accuracy.
  - Enhance the UI/UX to improve user engagement and interactivity.

### Applications of the Analysis
- **Impact**: Sentiment analysis can enhance user experience on music platforms by offering personalized recommendations based on emotional tone, mood, or preferences.

### Ethical Considerations
- Discuss potential privacy concerns regarding user data collection.
- Evaluate the ethical implications of using sentiment analysis in music recommendations.

---

### Refrences: 





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
