<link href='https://fonts.googleapis.com/css?family=Bungee' rel='stylesheet'>
<h2 style="font-family: 'Bungee', sans-serif; color: #00d0e3; font-size: 24px;">Sentiment Analysis on Spotify Data and Recommendation System</h2>

### Project Overview
This project aims to perform sentiment analysis on Spotify data to build a personalized recommendation system. By analyzing the emotional qualities of music, the project seeks to enhance personalized listening experiences and provide insights into user preferences.

#### Data Pipeline Flowchart

To give you a clear picture of how my Spotify sentiment analysis and recommendation system works, we've created a visual representation of my data pipeline. This flowchart illustrates the main steps of my process, from initial data collection to the final user interface. Let's take a look at the overall structure before we dive into the details of each component:

<div style="text-align: center;">
    <img src="images/spotify_project/flowchart.png?raw=true" width="300"/>
</div>

This flowchart outlines the five main stages of the pipeline:

1. Data Collection (Blue): We start by gathering data from two primary sources - the Spotify API for user listening history and the Genius API for song lyrics.

2. Data Processing (Green): In this stage, we clean and prepare our data. This involves removing duplicates from the Spotify data and cleaning the lyrics obtained from Genius.

3. Sentiment Analysis (Orange): Here, we use a RoBERTa model to analyze the cleaned lyrics and classify the emotions expressed in each song.

4. Recommendation Engine (Purple): This is where the magic happens. We combine mood-based filtering with popularity scoring to generate personalized song recommendations.

5. User Interface (Red): Finally, we present our results to the user. They can select their current mood, and our system will display tailored song recommendations.

As we progress through this post, we'll delve deeper into each of these stages, exploring the challenges we faced and the solutions we implemented. This flowchart will serve as our roadmap, helping you understand how each piece fits into the larger puzzle of my sentiment-based music recommendation system.

### The Data
**Timeframe**: April 2016 - August 2024 

**Attributes**: Musical history data, including track names, artists, genres, tempo, release date, lyrics, and sentiment scores

### Motivation & Hypothesis: 
Understanding the emotional impact of music is essential in today’s music landscape. This analysis aims to uncover how sentiment influences music preferences and listener engagement, ultimately leading to a more personalized recommendation system.

### Key Focus Areas

#### Data Ingestion
- **Overview**: Gathered historical musical data from Spotify using the Spotify API.
- **Steps Taken**: 
  - Collected personal listening history, including track metadata (name, artist, album, duration).
  - Filtered and removed duplicate songs to ensure data integrity.
- **Tools Used**: 
  - **Libraries**: `spotipy` (for Spotify API interaction), `pandas` (for data manipulation), and `numpy` (for numerical operations).
  - **Method**: Deduplication was handled using pandas' `drop_duplicates()` method.

#### Lyrics Fetching
- **Approach**: Fetched song lyrics via the Genius API by matching track names and artist information. 
- **Challenges**:
  - Faced API rate limits, which required batching requests.
  - Some API responses were slow or incomplete, leading to missing lyrics.

#### Data Cleaning
- **Method**: Used regular expressions (regex) to clean up the fetched lyrics, removing unwanted characters and formatting anomalies (e.g., brackets, newlines, special symbols). The code cleans song lyrics by removing metadata and non-ASCII characters, fetches them from the Genius API while caching results to prevent redundant calls, and processes a DataFrame to ensure only valid, clean lyrics are retained, eliminating any unwanted special characters. Additionally, it includes a delay to respect API rate limits
- **Example**:
  - **Raw**: "[Verse 1] I’m walking on sunshine! (Yeah, yeah)"
  - **Cleaned**: "I'm walking on sunshine"
- This cleaning process was essential to prepare the lyrics for sentiment analysis.

#### Code Snippet of Data Preparation: 
```python
def clean_lyrics(lyrics):
    # Remove anything within square brackets (like [Chorus], [Verse])
    lyrics = re.sub(r'\[.*?\]', '', lyrics)
    # Remove phrases indicating contributors to the lyrics (case insensitive)
    lyrics = re.sub(r'\b\d+\s+contributor(?:s)?\b', '', lyrics, flags=re.IGNORECASE)
    # Remove the word 'translation'
    lyrics = re.sub(r'\btranslation\b', '', lyrics, flags=re.IGNORECASE)
    # Remove any non-ASCII characters (such as emojis or special symbols)
    lyrics = re.sub(r'[^\x00-\x7F]+', '', lyrics)
    # Remove empty lines from the lyrics
    lyrics = '\n'.join([line for line in lyrics.split('\n') if line.strip()])
    return lyrics.strip()  # Return the cleaned lyrics, stripped of extra spaces
```
#### Sentiment Analysis
**Implementation**: Utilized a pre-trained transformer model from Hugging Face with PyTorch for sentiment analysis. In this post, we’ll explore how to analyze the emotions expressed in song lyrics using a machine-learning model. We’re working with a model called [roberta-base-go_emotions](https://huggingface.co/SamLowe/roberta-base-go_emotions?text=My+job+search+is+horrible+and+leading+nowhere) (click the link to see more detailed documentation on HuggingFace), which can identify 28 different emotions based on the lyrics (e.g. Love, Anger, Fear, etc.) provided, giving richer detail than a simple "Positive", "Negative" and "Neutral" assessment. However, this model has a limitation: it can only process up to 512 tokens (words or parts of words) at a time.

To get around this limitation, we use a technique called the sliding window approach using PyTorch. This method involves breaking the lyrics into overlapping sections, allowing us to analyze the entire song, even if it exceeds 512 tokens. The result is a clear understanding of the emotions in the lyrics, which can be useful for artists, producers, and fans alike.


#### Code Snippet of Sentiment Analysis Window Function: 
```python
import torch
from transformers import AutoTokenizer, AutoModelForSequenceClassification
import pandas as pd
from torch.nn.functional import softmax

# Load the tokenizer and model for emotion classification
tokenizer = AutoTokenizer.from_pretrained('SamLowe/roberta-base-go_emotions')
model = AutoModelForSequenceClassification.from_pretrained('SamLowe/roberta-base-go_emotions')
model.to('cuda' if torch.cuda.is_available() else 'cpu')

def sliding_window_sentiment_analysis(text, window_size=512, stride=256):
    # Tokenize and prepare input tensors
    inputs = tokenizer(text, return_tensors='pt', truncation=False)
    input_ids = inputs['input_ids'].squeeze()

    # Calculate number of sliding windows
    num_windows = max(1, (input_ids.size(0) - window_size) // stride + 1)
    all_logits = []

    # Process each sliding window
    for i in range(num_windows):
        window_input_ids = input_ids[i*stride:i*stride + window_size].unsqueeze(0)
        attention_mask = torch.ones_like(window_input_ids).to(model.device)

        with torch.no_grad():
            outputs = model(window_input_ids, attention_mask=attention_mask)
        all_logits.append(outputs.logits)

    # Average the logits and compute probabilities
    aggregated_logits = torch.mean(torch.stack(all_logits), dim=0)
    probs = softmax(aggregated_logits, dim=1)

    # Get predicted class and confidence score
    predicted_class = torch.argmax(probs).item()
    confidence = probs[0][predicted_class].item()

    return model.config.id2label[predicted_class], confidence

# Example usage
lyrics_list = df['Lyrics_Clean'].astype(str).tolist()
results = [{'label': sliding_window_sentiment_analysis(lyrics)[0], 
            'score': sliding_window_sentiment_analysis(lyrics)[1]} for lyrics in lyrics_list]

# Convert results to a DataFrame
lyrics_sentiment = pd.DataFrame(results)
print(lyrics_sentiment)

# Add sentiment results to the original DataFrame
df['Sentiment_Label'] = lyrics_sentiment['label']
df['Sentiment_Score'] = lyrics_sentiment['score']
</code>
</pre>
```
- **Results**: Classified song lyrics into one of 28 distinct sentiment categories (Love, Fear, Disappointment, Sadness, Nervousness, Annoyance, Disapproval, Disgust, Neutral, ... Relief, Gratitude, Pride), forming the basis for the mood-based recommendation system. The model assigned a sentiment based on the sentiment with the highest probability of being present among the 28 emotions the model was trained on. 

#### Recommendation System
- **Concept**: Built a bespoke, popularity, release date and mood-based recommendation engine where users pick a mood, and the system recommends songs based on historical sentiment analysis of lyrics.
- **Algorithm**: 
In this part of the project, we focus on recommending songs based on the user’s chosen mood or sentiment. The system uses the Spotify API to fetch song details and applies a custom popularity score based on how recently the song was released. This recommendation system is inspired by this [post](https://medium.com/@obielinda/building-a-spotify-recommendation-system-d4b67018eac2). Here’s a breakdown of the key features:

In this part of the project, the goal is to recommend songs based on the user’s selected mood or sentiment. The system gathers song details using the Spotify API and ranks them by how recently they were released, giving more weight to newer songs. Here’s a summary of the key features:

- **Popularity Based on Release Date**: The system assigns a score to each song depending on how recently it was released. Newer songs receive higher scores, ensuring the recommendations highlight recent music while still including older tracks.

- **Normalizing Song Features**: To make recommendations more accurate, the system adjusts different audio features—such as danceability, energy, and mood—so they are comparable. This helps in providing more balanced song suggestions.

- **Fetching Detailed Song Information**: Using the Spotify API, the system pulls up detailed song information like the song title, artist, Spotify link, album cover, and a short preview. This adds more context to the recommendations.

- **Mood-Based Recommendations**: The system filters songs based on their mood (or sentiment), giving users music that aligns with the emotional tone they’ve selected. This ensures the recommendations match the user’s current feeling.

- **Combining Mood and Popularity**: In addition to matching the mood, the system considers how popular the song is. It combines the mood-based suggestions with the popularity score to give a more balanced recommendation list.

- **User-Friendly Mood Selection**: A simple dropdown menu allows users to select their mood, and the system instantly shows songs that fit their emotional state.

This approach creates a dynamic recommendation system that not only tailors music to your mood but also keeps the results fresh by prioritizing newer tracks.

---

#### Key Code Snippet

```python
# Calculate weighted popularity based on release date
def calculate_weighted_popularity(release_date):
    release_date = datetime.strptime(release_date, '%Y-%m-%d')
    time_span = datetime.now() - release_date
    weight = 1 / (time_span.days + 1)  # Newer songs get a higher score
    return weight
```

**What It Does**:
1. **Parse Release Date**: Converts the song's release date from a string to a date format.
2. **Calculate Time Span**: Determines how many days have passed since the song was released.
3. **Assign Weight**: Recent songs get a higher score using the formula `1 / (time_span.days + 1)`. Older songs get lower scores, but are still included in the recommendations.

This calculation helps balance between recommending popular songs and suggesting newer tracks that fit the user’s mood and filtering based on sentiment. 

#### Interactive HTML Page

- **Design**: 
  - Created an intuitive HTML page where users can select an emotion from a list.
  - Users are presented with a carousel of song recommendations featuring album art, a preview of the song, and links to listen on Spotify.
- **Functionality**: 
  - The page dynamically generates recommendations based on user sentiment input, enhancing the user experience with personalized music choices.

#### UX Considerations for Carousel Design
- Focused on intuitive navigation and accessibility.
- Ensured a visually appealing, engaging layout for users.
- Provided clear feedback when users select an emotion or interact with the carousel.

<img src="images/mood_ring_final.gif?raw=true" width="1000"/>

**Prototype Available**: Check out the mood-based recommendation system prototype by clicking below!

<nav style="text-align: center;">
  <div style="display: inline-block; background-color: #ffe6f5; border-radius: 25px; padding: 10px 20px; box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);">
    <a href="mood_ring.html" style="font-family: 'Bagel Fat One', sans-serif; font-size: 42px; background: linear-gradient(90deg, #ff6666, #ffb366, #66ff66, #33ccff, #6699ff, #cc99ff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; text-decoration: none;">
      V's Musical Mood Ring
    </a>
  </div>
</nav>
<br> <br>

---

#### Next Steps
- **Improvements**:
  - Fine-tune the recommendation algorithm for better accuracy.
  - Enhance the UI/UX to improve user engagement and interactivity.

#### Applications of the Analysis
- **Impact**: Sentiment analysis can enhance user experience on music platforms by offering personalized recommendations based on emotional tone, mood, or preferences.

#### Ethical Considerations
- Discuss potential privacy concerns regarding user data collection.
- Evaluate the ethical implications of using sentiment analysis in music recommendations.

---





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
