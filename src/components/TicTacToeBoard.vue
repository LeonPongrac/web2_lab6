<template>
    <div>
      <div class="status">{{ status }}</div>
      <div class="board">
        <Square
          v-for="(value, index) in squares"
          :key="index"
          :value="value"
          @click="handleClick(index)"
        />
      </div>
    </div>
  </template>
  
  <script>
import { ref, computed, onMounted } from 'vue';
import Square from './Square.vue';

export default {
  components: {
    Square,
  },
  data() {
    return {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  },
  computed: {
    status() {
      return `Next player: ${this.xIsNext ? 'X' : 'O'}`;
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
        return squares[a]; // Return 'X' or 'O' as the winner
        }
    }

    return null; // No winner yet
        },
  },
  onMounted() {
    console.log('Board component mounted');
  },
};
</script>

<style scoped>
/* Add your scoped styles here */
.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  gap: 5px;
  margin: 20px auto; /* Center horizontally and add top margin */
  max-width: 300px; /* Set a max width to prevent the board from taking the full width */
}

.status {
  font-size: 1.5em;
  margin-bottom: 10px;
  text-align: center; /* Center the status text */
}
</style>

  