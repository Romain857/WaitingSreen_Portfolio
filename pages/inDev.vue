<template>
  <div>
    <OpeningAnimation 
      :fullName="fullName"
      v-show="!animationCompleted"
      @animation-completed="onAnimationCompleted"
    />
    <div v-show="animationCompleted">
      <Bubbles :bubbles="bubbles" ref="bubblesRef" />
    </div>
  </div>
</template>

<script>
import OpeningAnimation from '@/components/OpeningAnimation.vue';
import Bubbles from '@/components/Bubbles.vue';

export default {
  components: {
    OpeningAnimation,
    Bubbles
  },
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
                '<a href="https://github.com/Romain857" target="_blank" class="hover:text-gray-800 text-blue-500">GitHub</a> | ' +
                '<a href="https://www.linkedin.com/in/romain-martineau-8570/" target="_blank" class="hover:text-gray-800 text-blue-500">LinkedIn</a>' 
        },
        { text: 'See you soon 🚀' },
        { text: 'R. Martineau' }
      ]
    };
  },
  methods: {
    onAnimationCompleted() {
      this.animationCompleted = true;
      this.$nextTick(() => {
        this.$refs.bubblesRef.animateBubbles();
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
</style>