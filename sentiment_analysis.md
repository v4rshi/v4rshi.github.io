<link href='https://fonts.googleapis.com/css?family=Bungee' rel='stylesheet'>
<h2 style="font-family: 'Bungee', sans-serif; color: #00d0e3; font-size: 24px;">Sentiment Analysis on Spotify Data and Recommendation System</h2>

<style>
.zoom {
  transition: transform 0.5s ease;
}
.zoom.zoomed {
  transform: scale(2.5);
}
</style>


## Project Overview
This project aims to perform sentiment analysis on Spotify data to build a personalized recommendation system. By analyzing the emotional qualities of music, the project seeks to enhance personalized listening experiences and provide insights into user preferences.

### Data Pipeline Flowchart

To provide a clear picture of how our Spotify sentiment analysis and recommendation system works, we've created a visual representation of the data pipeline. This flowchart illustrates the main steps of our process, from initial data collection to the final user interface:

<div style="text-align: center;">
    <img src="images/spotify_project/flowchart.png?raw=true" width="300" class="zoom" alt="Zoomable Image"/>
</div>

1. **Data Collection (Blue)**: We begin by gathering data from two primary sources - the Spotify API for user listening history and the Genius API for song lyrics.

2. **Data Processing (Green)**: In this stage, we clean and prepare our data. This involves removing duplicates from the Spotify data and cleaning the lyrics obtained from Genius.

3. **Sentiment Analysis (Orange)**: Here, we use a RoBERTa model to analyze the cleaned lyrics and classify the emotions expressed in each song.

4. **Recommendation Engine (Purple)**: This is where the magic happens. We combine mood-based filtering with popularity scoring to generate personalized song recommendations.

5. **User Interface (Red)**: Finally, we present our results to the user. They can select their current mood, and our system will display tailored song recommendations.

## The Data

- **Timeframe**: April 2016 - August 2024
- **Attributes**: Musical history data, including track names, artists, genres, tempo, release date, lyrics, and sentiment scores

## Motivation & Hypothesis: 
Understanding the emotional impact of music is essential in today’s music landscape. This analysis aims to uncover how sentiment influences music preferences and listener engagement, ultimately leading to a more personalized recommendation system.

## Key Focus Areas

### 1. Data Ingestion

**Overview**: We gathered historical musical data from Spotify using the Spotify API.

**Steps Taken**:
- Collected personal listening history, including track metadata (name, artist, album, duration).
- Filtered and removed duplicate songs to ensure data integrity.

**Tools Used**:
- Libraries: spotipy (for Spotify API interaction), pandas (for data manipulation), and numpy (for numerical operations).
- Method: Deduplication was handled using pandas' `drop_duplicates()` method.

### 2. Lyrics Fetching

**Approach**: We fetched song lyrics via the Genius API by matching track names and artist information.

**Challenges**:
- Faced API rate limits, which required batching requests.
- Some API responses were slow or incomplete, leading to missing lyrics.

### 3. Data Cleaning

**Method**: We used regular expressions (regex) to clean up the fetched lyrics, removing unwanted characters and formatting anomalies (e.g., brackets, newlines, special symbols).

**Example**:
- Raw: `"[Verse 1] I'm walking on sunshine! (Yeah, yeah)"`
- Cleaned: `"I'm walking on sunshine"`

This cleaning process was essential to prepare the lyrics for sentiment analysis.

Here are some before and after images: 

<div style="display: flex; justify-content: center;">
    <div style="margin-right: 10px; text-align: center;">
        <img src="images/spotify_project/Lyrics Before.png?raw=true" width="300" class="zoom" alt="Zoomable Image"/>
        <p>Lyrics Before Cleaning</p>
    </div>
    <div style="text-align: center;">
        <img src="images/spotify_project/Lyrics After.png?raw=true" width="300" class="zoom" alt="Zoomable Image"/>
        <p>Lyrics After Cleaning</p>
    </div>
</div>

**Note**: I also had to identify if the Genius API scraped something that did not look like lyrics entirely. Here are some examples of that: 

<div style="display: flex; justify-content: center;">
    <div style="margin-right: 10px; text-align: center;">
        <img src="images/spotify_project/nonsense_1.png?raw=true" width="300" class="zoom" alt="Zoomable Image"/>
        <p>Track Names and Artist Names</p>
    </div>
    <div style="text-align: center;">
        <img src="images/spotify_project/nonsense_2.png?raw=true" width="300" class="zoom" alt="Zoomable Image"/>
        <p>Track Names and Artist Names as Lists</p>
    </div>
</div>

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


## Sentiment Analysis
**Implementation**: Utilized a pre-trained transformer model from Hugging Face with PyTorch for sentiment analysis. In this post, we’ll explore how to analyze the emotions expressed in song lyrics using a machine-learning model. We’re working with a model called [roberta-base-go_emotions](https://huggingface.co/SamLowe/roberta-base-go_emotions?text=My+job+search+is+horrible+and+leading+nowhere) (click the link to see more detailed documentation on HuggingFace), which can identify 28 different emotions based on the lyrics (e.g. Love, Anger, Fear, etc.) provided, giving richer detail than a simple "Positive", "Negative" and "Neutral" assessment. However, this model has a limitation: it can only process up to 512 tokens (words or parts of words) at a time.

To get around this limitation, we use a technique called the sliding window approach using PyTorch. This method involves breaking the lyrics into overlapping sections, allowing us to analyze the entire song, even if it exceeds 512 tokens. The result is a clear understanding of the emotions in the lyrics, which can be useful for artists, producers, and fans alike.


### Code Snippet of Sentiment Analysis Window Function: 


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
```
### Explanation of the Sliding Window Method

1. The process starts with a long text input (like song lyrics).
2. The text is split into overlapping windows. Typically, the window size is 512 tokens, and the stride (overlap) is 256 tokens.
3. Each window is processed separately by the sentiment analysis model.
4. The results from all windows are averaged to get the final sentiment.

The "Sliding Window Process" subgraph at the bottom shows how the windows overlap:

- Window 1 covers the first chunk of text.
- Window 2 starts halfway through Window 1 and covers the next chunk.
- Window 3 starts halfway through Window 2 and covers the next chunk.

This process continues until the entire text is covered. By using overlapping windows, the algorithm ensures that no part of the text is analyzed in isolation, which helps to maintain context throughout the analysis.


<div style="text-align: center;">
    <img src="images/spotify_project/sliding_window.png?raw=true" width="300" class="zoom" alt="Zoomable Image"/>
</div>

### Sliding Window Implementation Details

The main steps in the code that implement this process are:

1. The `sliding_window_sentiment_analysis` function processes the text in chunks.
2. It calculates the number of windows based on the text length, window size, and stride.
3. For each window, it runs the sentiment analysis model and stores the results.
4. Finally, it averages the results from all windows to get the final sentiment and confidence score.

This technique is particularly useful for long texts that exceed the maximum input size of the sentiment analysis model, allowing for comprehensive analysis of the entire text while maintaining local context.

- **Results**: Classified song lyrics into one of 28 distinct sentiment categories (Love, Fear, Disappointment, Sadness, Nervousness, Annoyance, Disapproval, Disgust, Neutral, ... Relief, Gratitude, Pride), forming the basis for the mood-based recommendation system. The model assigned a sentiment based on the sentiment with the highest probability of being present among the 28 emotions the model was trained on. 

<iframe src="images/spotify_project/sentiment_bar_chart" style="width: 100%; height: calc(100vw * 3 / 4);"></iframe>

From the visualization, I noticed that the "Neutral" sentiment dominates, which aligns with my observation that the Genius API did not always consistently scrape lyrics correctly. This prevalence of neutral sentiment suggests there may be some areas for improvement in my data extraction and cleaning process. After reflecting on the results, I've come up with a few possible reasons and ideas for refinement:

1. **Data granularity:**  
   My current sentiment analysis might not be capturing the full emotional depth of the lyrics. To address this, I could try a more fine-grained emotion classification model or adjust the thresholds for what gets labeled as neutral.

2. **Context sensitivity:**  
   Song lyrics often use metaphors, irony, and complex emotional themes that general-purpose sentiment analysis models might struggle to interpret. Fine-tuning my model on a dataset specific to song lyrics could help improve its accuracy.

3. **Sliding window approach:**  
   I’m currently using a sliding window to analyze sentiment and then averaging across the windows. This might be smoothing out more pronounced emotions in certain parts of the lyrics. I could experiment with different aggregation methods, like using the maximum sentiment score instead of the average, to capture these more intense emotions.

4. **Preprocessing:**  
   It’s also possible that my data cleaning process is unintentionally stripping out important emotional cues. I plan to review my preprocessing steps to ensure I’m not neutralizing text that holds meaningful sentiment.

5. **Model selection:**  
   I’m using the 'SamLowe/roberta-base-go_emotions' model, which might not be the best fit for analyzing song lyrics. I could experiment with other pre-trained models that are better suited for detecting emotions in creative, lyrical text.

6. **Threshold adjustment:**  
   Another option is adjusting the threshold for classifying sentiment as neutral. By setting a higher minimum confidence score for non-neutral classifications, I might reduce the number of lyrics labeled as neutral.

### How I plan to refine my analysis:
- Experimenting with different pre-trained models or fine-tuning the current model on a dataset of labeled song lyrics.
- Tweaking the sliding window parameters (window size and stride) to see if that improves how well sentiment is captured.
- Trying a more sophisticated aggregation method to better combine sentiments across different windows.
- Reviewing and refining the data cleaning process to ensure that important emotional cues in the lyrics are preserved.
- Exploring a multi-label classification approach, where a song can have multiple sentiment labels, each with varying intensities.

Sentiment analysis of song lyrics is a tricky task because of the creative and often ambiguous nature of the text. I know it’ll take some trial and error, but I’m confident that with a few more iterations, I’ll be able to improve the accuracy of my results.


## Recommendation System
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

### Key Code Snippet

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

### UX Considerations for Carousel Design
- Focused on intuitive navigation and accessibility.
- Ensured a visually appealing, engaging layout for users.
- Provided clear feedback when users select an emotion or interact with the carousel.

<img src="images/mood_ring_final.gif?raw=true" width="1000" class="zoom" alt="Zoomable Image"/>

**Prototype Available**: Check out the mood-based recommendation system prototype by clicking below!

<nav style="text-align: center;">
  <div style="display: inline-block; background-color: #ffe6f5; border-radius: 25px; padding: 10px 20px; box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);">
    <a href="mood_ring.html" style="font-family: 'Bagel Fat One', sans-serif; font-size: 42px; background: linear-gradient(90deg, #ff6666, #ffb366, #66ff66, #33ccff, #6699ff, #cc99ff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; text-decoration: none;">
      V's Musical Mood Ring
    </a>
  </div>
</nav>
<br> 

---

## Next Steps
- **Improvements** : Moving forward, I plan to fine-tune the recommendation algorithm to improve its accuracy. Additionally, I want to enhance the UI/UX to boost user engagement and interactivity, ensuring the platform feels more intuitive and enjoyable to use.

- **Applications of the Analysis** : The sentiment analysis I’ve developed has the potential to make a meaningful impact by improving user experience on music platforms. Personalized recommendations based on emotional tone, mood, or individual preferences could transform how users discover music, making it feel more tailored to their current feelings and needs.

- **Ethical Considerations** : As with any project involving user data, privacy concerns are a key issue to consider. I’ll be looking into ways to address these concerns responsibly, ensuring that user data is protected. It’s also important to evaluate the broader ethical implications of applying sentiment analysis in music recommendations, such as the potential for reinforcing certain moods or behaviors, and how to avoid biases in the recommendation system.


---





<link href='https://fonts.googleapis.com/css?family=Bagel Fat One' rel='stylesheet'>


<style>
  nav a:hover {
    color: #00ff00; /* Brighter green */
  }
</style>

<link href='https://fonts.googleapis.com/css?family=Bungee Shade' rel='stylesheet'>

<script>
document.addEventListener('DOMContentLoaded', function() {
  document.querySelectorAll('.zoom').forEach(function(element) {
    element.addEventListener('click', function() {
      this.classList.toggle('zoomed');
    });
  });
});
</script>


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
