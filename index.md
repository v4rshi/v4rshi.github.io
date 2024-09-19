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
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(255, 255, 255, 0.7);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.3s ease;
    border-radius: 30px;
  }
  .project-title {
    font-family: 'Days One', sans-serif;
    text-align: center;
    color: #5fc400;
    font-size: 18px;
    margin: 0;
    padding: 10px;
  }
  .project-container:hover .overlay {
    opacity: 1;
  }
</style>

<link href='https://fonts.googleapis.com/css?family=Bungee+Shade|Black+Han+Sans|Days+One' rel='stylesheet'>

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
