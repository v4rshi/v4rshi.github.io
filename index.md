<style>
  .project-container {
    position: relative;
    display: flex;
    justify-content: center; /* Center the container */
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 20px;
    width: 100%; /* Set the container width to be responsive */
  }
  .project-image {
    border-radius: 30px;
    overflow: hidden;
    border: 5px solid white;
    display: block;
    max-width: 100%; /* Ensure the image scales responsively */
    height: auto;
  }
  .overlay {
    position: absolute;
    top: -5px;
    left: -5px;
    right: -5px;
    bottom: -5px;
    background-color: rgba(255, 255, 255, 0.75);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.15s ease;
    border-radius: 35px;
  }
  .project-title {
    font-family: 'Jost', sans-serif;
    text-align: left; /* Left-align the h3 text */
    color: #EC3B83;
    font-size: 28px;
    margin: 0;
    padding: 20px;
    text-shadow: 0 0 10px rgba(255, 255, 255, 0.8),
                 0 0 20px rgba(255, 255, 255, 0.8),
                 0 0 30px rgba(255, 255, 255, 0.8);
    letter-spacing: 1px;
  }
  .project-container:hover .overlay {
    opacity: 1;
  }
</style>

<link href='https://fonts.googleapis.com/css?family=Bungee+Shade|Black+Han+Sans|Bebas+Neue|Jost' rel='stylesheet'>

# <span style="font-family: 'Bungee Shade', sans-serif; color: #9760ce; font-size: 30px;">Portfolio</span>

## <span style="font-family: 'Bungee Shade', sans-serif; color: #04c3d1; font-size: 24px;">Data Analytics Projects</span>

<div class="project-container">
  <a href="https://v4rshi.github.io/seasons_eda.html">
    <img src="images/spotify_project/seasons_eda.gif?raw=true" alt="Seasons EDA" class="project-image">
    <div class="overlay">
      <h3 class="project-title">Analyzing 9 years of Spotify Data</h3>
    </div>
  </a>
</div>

<div class="project-container">
  <a href="https://v4rshi.github.io/sentiment_analysis.html">
    <img src="images/spotify_project/sentiment_analysis.gif?raw=true" alt="Sentiment Analysis" class="project-image">
    <div class="overlay">
      <h3 class="project-title">Sentiment Analysis on Spotify Data</h3>
    </div>
  </a>
</div>

<p style="font-size:9px">© Copyright of Varshini Srinivas</p>
