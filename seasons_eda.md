## Storytime with Spotify Data 

**Project Description**: I was able to get playlist data for my Spotify playlists thanks to a website called [Exportify](https://exportify.net/). It made me wonder, can I use this data to understand my mood and well-being over the years based on the season of the year I listened to something and the sentiment of the songs (name and lyrics) themselves?

**Data**: My dataset spans from April 2016 to August 2024. Each entry contains rich metadata including artist, track, addition date, and genre.

**Motivation & Hypothesis**: This dataset captures a transformative period in my life. From relocating from Dubai to Indiana for college, navigating the global pandemic (and graduate school in lockdown), experiencing personal losses, moving to San Francisco, starting my career, meeting my now husband and getting married, and transitioning between jobs. Throughout these experiences, Spotify remained a constant companion.

I've observed that my playlists often serve as a form of musical journaling, reflecting my emotional state and circumstances. This project aims to analyze the evolution of my musical preferences over time and explore potential correlations between playlist characteristics (content, length, addition frequency) and my emotional well-being.

Key focus areas for this project include:

1. Temporal analysis of musical taste to confirm if the data reveals what I think know (or do not know) about my musical taste 
2. Seasonal patterns in playlist composition, particularly relative to seasons and whatever weather changes they bring
3. Sentiment analysis of song lyrics, with a specific focus on the period of July 2023 to now (coinciding with my period of unemployment)

By examining these data points, I hope to uncover insights into how my music choices have mirrored my life experiences and emotional states during this pivotal time. 

##### **It is important to note that this data did not include how often I listened to specific songs, just when I added them to a given playlist. This data would be great for a more in-depth analysis of my listening patterns.**
---

### 1. The first thing I looked at was who my most listened to artists were.
I was fully expecting my top artist to be Charli XCX but in a rather surprising turn of events, its Future??? I did not see this in my Future, that is for sure.

```javascript
def count_artists(df):
    # Ensure the 'Artist Name(s)' column is treated as a string
    df['Artist Name(s)'] = df['Artist Name(s)'].astype(str)
    
    # Split artist names by comma and explode the lists into separate rows
    df_exploded = df['Artist Name(s)'].str.split(',', expand=True).stack()
    df_exploded = df_exploded.reset_index(drop=True).str.strip()  # Remove extra spaces

    # Count occurrences of each artist
    artist_counts = df_exploded.value_counts()

    return artist_counts

# Assuming df_subset is your DataFrame
artist_counts = count_artists(df_subset[['Artist Name(s)']])

# Sort artists by count (descending) and get top 20
top_artists = artist_counts.nlargest(20)
```

### 2. Assess assumptions on which statistical inference will be based

```javascript
if (isAwesome){
  return true
}
```

### 3. Support the selection of appropriate statistical tools and techniques

<img src="images/dummy_thumbnail.jpg?raw=true"/>

### 4. Provide a basis for further data collection through surveys or experiments

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
