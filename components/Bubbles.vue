<template>
  <div class="bubble-container">
    <div class="flex flex-col space-y-4">
      <div class="relative" v-for="(bubble, index) in bubbles" :key="index">
        <div class="absolute bg-white rounded-lg px-4 py-3 shadow-md opacity-0 bubble-scale"
             :style="{ top: `${index * 70}px`, left: '20px' }">
          <p class="text-2xl text-gray-800" v-html="bubble.text"></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import anime from 'animejs/lib/anime.es.js';

export default {
  props: ['bubbles'],
  methods: {
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
.bubble-container {
  position: relative;
  padding: 10px;
}
</style>