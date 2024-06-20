<template>
  <div>
    <div class="opening-animation" ref="openingAnimation" v-show="!animationCompleted">
      <div class="text-wrapper">
        <h1 class="letters" style="margin-top: -20px;">
          <span v-for="(char, index) in formattedFullName" :key="index" :class="['letter', { 'space': char === ' ' }]">
            {{ char }}
          </span>
        </h1>
      </div>
    </div>
    <div v-show="animationCompleted" class="bubble-container">
      <div class="flex flex-col space-y-4">
        <div class="relative" v-for="(bubble, index) in bubbles" :key="index">
          <div class="absolute bg-white rounded-lg px-4 py-3 shadow-md opacity-0 bubble-scale"
               :style="{ top: `${index * 70}px`, left: '20px' }">
            <p class="text-2xl text-gray-800" v-html="bubble.text"></p>
          </div>
        </div>
      </div>
      <Nuxt />
    </div>
  </div>
</template>

<script>
import anime from 'animejs/lib/anime.es.js';

export default {
  data() {
    return {
      fullName: "Romain Martineau's Portfolio",
      animationCompleted: false,
      bubbles: [
        { text: 'Hello 👋' },
        { text: 'My name is Romain' },
        { text: "I'm a fullstack developer currently looking for a new experience for 2025" },
        { text: "My portfolio is currently in development" },
        { 
          text: 'In the meantime, you can discover my profile and contact me on various platforms: ' +
                '<a href="https://github.com/Romain857" target="_blank" class="hover:text-gray-800 text-blue-500"></i>GitHub</a> | ' +
                '<a href="https://www.linkedin.com/in/romain-martineau-8570/" target="_blank" class="hover:text-gray-800 text-blue-500"></i>LinkedIn</a>' 
        },
        { text: 'See you soon 🚀' },
        { text: 'R. Martineau' }
      ]
    };
  },
  computed: {
    formattedFullName() {
      return this.fullName.split('');
    }
  },
  mounted() {
    this.animateOpening();
  },
  methods: {
    animateOpening() {
      anime.timeline({ loop: false })
        .add({
          targets: '.opening-animation .letter',
          translateY: [100, 0],
          opacity: [0, 1],
          easing: "easeOutExpo",
          duration: 1200,
          delay: (el, i) => 30 * i
        })
        .add({
          targets: '.opening-animation .letter',
          translateY: [0, -100],
          opacity: [1, 0],
          easing: "easeInExpo",
          duration: 1200,
          delay: (el, i) => 30 * i,
          complete: () => {
            this.animationCompleted = true;
            this.animateBubbles();
          }
        });
    },
    animateBubbles() {
      anime.timeline({ loop: false })
        .add({
          targets: '.bubble-scale',
          translateY: [-50, 0],
          opacity: [0, 1],
          easing: 'easeOutExpo',
          duration: 1000,
          delay: (el, i) => 900 * i
        });
    }
  }
}
</script>

<style scoped>
html, body {
  margin: 0;
  padding: 0;
  overflow: hidden;
}
.opening-animation {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background: #000;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  z-index: 9999;
}
.text-wrapper {
  overflow: hidden;
}
.letters {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.letter {
  display: inline-block;
  font-size: 3rem;
  font-weight: bold;
}
.space {
  width: 0.5em;
}
.bubble-container {
  position: relative;
  padding: 10px;
}
</style>