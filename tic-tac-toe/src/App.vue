<template>
  <div id="app">
    <div class="board">
      <div
        v-for="(cell, index) in board"
        :key="index"
        class="cell"
        @click="makeMove(index)"
      >
        {{ cell }}
      </div>
    </div>
    <button @click="resetGame">Restart Game</button>
    <p v-if="winner">{{ winner }} Wins!</p>
    <p v-if="draw && !winner">It's a Draw!</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      board: Array(9).fill(null),
      currentPlayer: 'X',
      winner: null,
      draw: false,
    };
  },
  methods: {
    makeMove(index) {
      if (!this.board[index] && !this.winner) {
        this.$set(this.board, index, this.currentPlayer);
        if (this.checkWinner()) {
          this.winner = this.currentPlayer;
        } else if (this.board.every(cell => cell)) {
          this.draw = true;
        } else {
          this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
        }
      }
    },
    checkWinner() {
      const winningCombination = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      return winningCombination.some(combination => {
        const [a, b, c] = combination;
        return this.board[a] && this.board[a] === this.board[b] && this.board[a] === this.board[c];
      });
    },
    resetGame() {
      this.board = Array(9).fill(null);
      this.currentPlayer = 'X';
      this.winner = null;
      this.draw = false;
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
  gap: 5px;
  justify-content: center;
}

.cell {
  width: 100px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2em;
  border: 1px solid #000;
  cursor: pointer;
}

button {
  margin-top: 20px;
  padding: 10px 20px;
}
</style>