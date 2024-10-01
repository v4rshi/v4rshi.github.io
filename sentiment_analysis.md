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
- **Method**: Used regular expressions (regex) to clean up the fetched lyrics, removing unwanted characters and formatting anomalies (e.g., brackets, newlines, special symbols). The code cleans song lyrics by removing metadata and non-ASCII characters, fetches them from the Genius API while caching results to prevent redundant calls, and processes a DataFrame to ensure only valid, clean lyrics are retained, eliminating any unwanted special characters. Additionally, it includes a delay to respect API rate limits
- **Example**:
  - **Raw**: "[Verse 1] I’m walking on sunshine! (Yeah, yeah)"
  - **Cleaned**: "I'm walking on sunshine"
- This cleaning process was essential to prepare the lyrics for sentiment analysis.

### Code Snippet of Data Preparation: 
```javascript
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
- **Implementation**: Utilized a pre-trained transformer model from Hugging Face (like `distilbert-base-uncased`) with PyTorch for sentiment analysis. In this post, we’ll explore how to analyze the emotions expressed in song lyrics using a machine-learning model. We’re working with a model called [roberta-base-go_emotions](https://huggingface.co/SamLowe/roberta-base-go_emotions?text=My+job+search+is+horrible+and+leading+nowhere) (click the link to see more detailed documentation on HuggingFace), which can identify different emotions based on the lyrics provided. However, this model has a limitation: it can only process up to 512 tokens (words or parts of words) at a time.

To get around this limitation, we use a technique called the sliding window approach using PyTorch. This method involves breaking the lyrics into overlapping sections, allowing us to analyze the entire song, even if it exceeds 512 tokens. The result is a clear understanding of the emotions in the lyrics, which can be useful for artists, producers, and fans alike.


### Code Snippet of Sentiment Analysis Window Function: 
```javascript
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

```

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
