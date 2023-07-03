<template>
  <div class="game-widget">
    <h2>Tic Tac Toe</h2>
    <div class="board">
      <div v-for="(cell, index) in cells" :key="index" class="cell" @click="makeMove(index)">
        {{ cell }}
      </div>
    </div>
    <button @click="resetGame">Reset Game</button>
    <p v-if="gameOver" class="result">{{ winnerMessage }}</p>
  </div>
</template>

<script>
export default {
  name: 'GameWidget',
  data() {
    return {
      currentPlayer: 'X',
      cells: Array(9).fill(''),
      gameOver: false,
      winner: ''
    };
  },
  computed: {
    currentPlayerMessage() {
      return `Current Player: ${this.currentPlayer}`;
    },
    winnerMessage() {
      return this.winner ? `Winner: ${this.winner}` : "It's a tie!";
    }
  },
  methods: {
    makeMove(index) {
      if (!this.gameOver && this.cells[index] === '') {
        this.cells[index] = this.currentPlayer;
        if (this.checkWinningCondition(this.currentPlayer)) {
          this.gameOver = true;
          this.winner = this.currentPlayer;
        } else if (!this.cells.includes('')) {
          this.gameOver = true;
        } else {
          this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
        }
      }
    },
    checkWinningCondition(player) {
      const winningConditions = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ];

      return winningConditions.some(condition =>
        condition.every(index => this.cells[index] === player)
      );
    },
    resetGame() {
      this.currentPlayer = 'X';
      this.cells = Array(9).fill('');
      this.gameOver = false;
      this.winner = '';
    }
  }
};
</script>

<style scoped>
.game-widget {
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
  text-align: center;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
  margin-bottom: 10px;
}

.cell {
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid #000000;
  font-size: 2em;
  cursor: pointer;
  height: 100px;
}

button {
  margin-top: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}

p.result {
  font-weight: bold;
  margin-top: 10px;
}
</style>
