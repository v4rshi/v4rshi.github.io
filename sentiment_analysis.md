<link href='https://fonts.googleapis.com/css?family=Days One' rel='stylesheet'>
<h2 style="font-family: 'Days One', sans-serif; color: #b171f1; font-size: 24px;">COMING SOON: Using LLM's to do Sentiment Analysis on song lyrics!</h2>

<link href='https://fonts.googleapis.com/css?family=Bagel Fat One' rel='stylesheet'>
I am still working out the kinks, but in the mean-time, I developed a mood-based recommendation system prototype - check it out! 

Click on the link below to explore my Musical Mood Ring! Select a 'Sentiment' to discover 5 songs with similar vibes.
<nav style="text-align: center;">
  <div>
    <a href="mood_ring.html" style="font-family: 'Bagel Fat One', sans-serif; color: #1DB954; font-size: 24px;">
      V's Musical Mood Ring
    </a>
  </div>
</nav>

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
