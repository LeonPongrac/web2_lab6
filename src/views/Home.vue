<template>
    <div>
    <Header />
    
    <main>
      <h2>Game Board</h2>
      <TicTacToeBoard />
    </main>
  </div>
  </template>
  
<script>
  import TicTacToeBoard from '@/components/TicTacToeBoard.vue';
  import Header from '@/components/Header.vue';
  
  export default {
    components: {
      TicTacToeBoard,
      Header,
    },
  };
</script>

<style scoped>
header {
  background-color: #f0f0f0;
  padding: 10px;
  text-align: center;
}

nav {
  margin-top: 10px;
}

nav a {
  margin-right: 10px;
}
</style>
  