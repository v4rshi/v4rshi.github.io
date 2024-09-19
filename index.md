---
layout: default
---

<style>
  .project-container {
    position: relative;
    display: inline-block;
    margin-left: 20px;
    margin-bottom: 20px;
  }
  .project-image {
    border-radius: 30px;
    overflow: hidden;
    border: 5px solid white;
    display: block;
    width: 1000px;
  }
  .overlay {
    position: absolute;
    top: -5px;
    left: -5px;
    right: -5px;
    bottom: -5px;
    background-color: rgba(255, 115, 180, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.15s ease;
    border-radius: 35px;
  }
  .project-title {
    font-family: 'Bebas Neue', sans-serif;
    text-align: center;
    color: #FFFFFF;
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

<link href='https://fonts.googleapis.com/css?family=Bungee+Shade|Black+Han+Sans|Bebas+Neue' rel='stylesheet'>

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
