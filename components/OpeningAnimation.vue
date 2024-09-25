<template>
  <div class="opening-animation" ref="openingAnimation" v-show="!animationCompleted">
    <div class="text-wrapper">
      <h1 class="letters" style="margin-top: -20px;">
        <span v-for="(char, index) in formattedFullName" :key="index" :class="['letter', { 'space': char === ' ' }]">
          {{ char }}
        </span>
      </h1>
    </div>
  </div>
</template>

<script>
import anime from 'animejs/lib/anime.es.js';

export default {
  props: ['fullName'],
  data() {
    return {
      animationCompleted: false,
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
            this.$emit('animation-completed');
          }
        });
    }
  }
}
</script>

<style scoped>
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
</style>