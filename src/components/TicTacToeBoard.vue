<template>
    <div>
      <div class="status">{{ gameStatus }}</div>
      <div class="board">
        <Square
          v-for="(value, index) in squares"
          :key="index"
          :value="value"
          @click="handleClick(index)"
        />
      </div>
      <ResetButton @reset="resetGame" />
    </div>
  </template>
  
<script>
  import { ref, computed, onMounted } from 'vue';
  import Square from './Square.vue';
  import ResetButton from './ResetButton.vue';

  export default {
    components: {
      Square,
      ResetButton,
    },
    data() {
      return {
        squares: Array(9).fill(null),
        xIsNext: Math.random() < 0.5,
      };
    },
    computed: {
      gameStatus() {
        const winner = this.calculateWinner(this.squares);

        if (winner) {
          return `Player ${winner} wins!`;
        } else if (this.squares.every((square) => square !== null)) {
          return 'Draw!';
        } else {
          return `Next player: ${this.xIsNext ? 'X' : 'O'}`;
        }
      },
    },
    methods: {
      handleClick(index) {
        if (this.calculateWinner(this.squares) || this.squares[index]) {
          return;
        }
        const squares = this.squares.slice();
        squares[index] = this.xIsNext ? 'X' : 'O';
        this.squares = squares;
        this.xIsNext = !this.xIsNext;
      },
      calculateWinner(squares) {
          const lines = [
          [0, 1, 2],
          [3, 4, 5],
          [6, 7, 8],
          [0, 3, 6],
          [1, 4, 7],
          [2, 5, 8],
          [0, 4, 8],
          [2, 4, 6],
      ];

      for (const line of lines) {
          const [a, b, c] = line;
          if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
          return squares[a];
          }
      }

      return null;
      },
        resetGame() {
        this.squares = Array(9).fill(null);
        this.xIsNext = Math.random() < 0.5;
      },
    },
    onMounted() {
      console.log('Board component mounted');
    },
  };
</script>

<style scoped>
.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  gap: 5px;
  margin: 20px auto;
  max-width: 300px;
}

.status {
  font-size: 1.5em;
  margin-bottom: 10px;
}
</style>

  