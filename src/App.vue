<template>
  <div>
    <button @click="toggleMusic" :class="{'music-btn': true, 'playing': isPlaying, 'paused': !isPlaying}"></button>

    <!-- Add the GIF here above the text -->
    <div class="gif-container">
      <img src="@/assets/peach1.gif" alt="Peach GIF" class="gif-image" />
    </div>

    <div class="text">
      <h1 class="fancy-font" @mouseenter="triggerConfetti">All The Best for Finals!</h1>
      <p class="fancy-font" @mouseenter="triggerSparkles">加油, Ting Ting!</p>
    </div>
  </div>

  <footer class="designed-by">
    Designed by <a href="https://mir-s3-cdn-cf.behance.net/project_modules/disp/90a5a548817043.58a2f52532541.gif" target="_blank" class="designed-by-link">Lucas</a>
  </footer>
</template>



<script>
import party from 'party-js';

export default {
  name: 'App',
  data() {
    return {
      isPlaying: false,
      audio: null,
    };
  },

  methods: {
    toggleMusic() {
      if (this.isPlaying) {
        this.audio.pause();
      } else {
        this.audio.play();
      }
      this.isPlaying = !this.isPlaying;
    },
    
    triggerConfetti() {
      const confettiSettings = {
        count: party.variation.range(20, 40),
        size: party.variation.range(0.6, 1.4)
      };
      party.confetti(document.querySelector('.fancy-font'), confettiSettings);
    },
    triggerSparkles() {
      const sparklesSettings = {
        count: party.variation.range(10, 60),
        speed: party.variation.range(50, 300)
      };
      party.sparkles(document.querySelector('.fancy-font'), sparklesSettings);
    }
  },

  mounted() {
    this.audio = new Audio(require('@/assets/music1.mp3')); // Ensure you have music1.mp3 in your assets folder
    this.effectInterval = setInterval(() => {
      this.triggerConfetti();
      setTimeout(this.triggerSparkles, 2500); // Triggers 2.5 seconds after confetti
    }, 5000);
  },
  beforeUnmount() {
    clearInterval(this.effectInterval); // Clear the interval when the component is destroyed
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Lato:300');

html, body {
  width: 100%;
  height: 100%;
  margin: 0; /* Remove default margin */
}

body {
  background: #FFB6C1; /* Soft pink color */
  display: flex; /* Use flexbox */
  justify-content: center; /* Center items horizontally */
  align-items: center; /* Center items vertically */
  height: 100vh; /* Full viewport height */
}

.fancy-font {
    font-family: 'Roboto', sans-serif;
    font-size: 5vw; /* Font size is 2% of the viewport's width */
    color: black;
    margin: 0;
    text-align: center;
    cursor: pointer; /* Adds a pointer cursor on hover */
}

@media (max-width: 600px) {
    .fancy-font {
        font-size: 12px; /* Minimum font size */
    }
}

@media (min-width: 1200px) {
    .fancy-font {
        font-size: 24px; /* Maximum font size */
    }
}

/* Center the GIF */
.gif-container {
  text-align: center; /* Centers the gif horizontally */
  margin-bottom: 20px; /* Adds some space between the gif and the text */
}

.gif-image {
  max-width: 20%; /* Ensures the gif scales with the screen */
  height: auto; /* Keeps the gif's aspect ratio intact */
}

.text {
  color: #8b6a60;
  font-family: 'Lato', sans-serif;
  font-weight: 100;
  text-align: center;
}

.designed-by {
    position: absolute;
    bottom: 2.5%;
    width: 100%;
    text-align: center;
    color: black;
    font-family: 'Roboto', sans-serif;
}

.designed-by-link{
  color: orange;
}

.music-btn {
  position: absolute;
  top: 16px;
  right: 16px;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background-color: #FFC0CB;
  border: 5px solid #000;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background-color 0.3s;
}

.music-btn.playing::before {
  content: '\f001';
  font-family: 'Material Design Icons';
  font-size: 24px;
  color: #000;
}

.music-btn.paused::after {
  content:
 '\f003';
  font-family: 'Material Design Icons';
  font-size: 24px;
  color: #000;
}
</style>

