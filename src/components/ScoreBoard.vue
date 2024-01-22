<template>
    <div class="score-board">
      <p>Player X: {{ scores.playerX }}</p>
      <p>Player O: {{ scores.playerO }}</p>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  import { useStore } from '@/store';
  
  export default {
    setup() {
      const store = useStore();
      const scores = ref(store.scores);
  
      return {
        scores,
      };
    },
  };
  </script>
  
  <style scoped>
  .score-board {
    margin-top: 20px;
  }
  </style>
  