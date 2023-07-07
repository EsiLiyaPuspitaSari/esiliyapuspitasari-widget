<template>
  <div class="container1">
    <h1>Tic Tac Toe</h1>
    <div class="board">
      <div class="row" v-for="(row, rowIndex) in rows" :key="rowIndex">
        <div class="cell" v-for="(cell, colIndex) in row" :key="colIndex" @click="makeMove(rowIndex, colIndex)">
          {{ cell }}
        </div>
      </div>
    </div>
    <button @click="resetBoard" :disabled="gameOver" class="button-tertiary">Reset</button>
    <button class="button-tertiary" @click="backToHome">Back To Home</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rows: [[null, null, null], [null, null, null], [null, null, null]],
      currentPlayer: 'X',
      gameOver: false
    };
  },
  methods: {
    makeMove(rowIndex, colIndex) {
      if (!this.gameOver && !this.rows[rowIndex][colIndex]) {
        this.rows[rowIndex][colIndex] = this.currentPlayer;
        if (this.checkWin(this.currentPlayer)) {
          alert(this.currentPlayer + ' wins!');
          this.gameOver = true;
        } else if (this.checkDraw()) {
          alert("It's a draw!");
          this.gameOver = true;
        } else {
          this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
        }
      }
    },
    backToHome() {
      this.$router.push('/');
    },
    checkWin(player) {
      const winningCombinations = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8], // rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8], // columns
        [0, 4, 8], [2, 4, 6] // diagonals
      ];
      return winningCombinations.some(combination => {
        return combination.every(index => {
          const [rowIndex, colIndex] = this.getCellPosition(index);
          return this.rows[rowIndex][colIndex] === player;
        });
      });
    },
    checkDraw() {
      return this.rows.every(row => row.every(cell => cell !== null));
    },
    resetBoard() {
      this.rows = [[null, null, null], [null, null, null], [null, null, null]];
      this.currentPlayer = 'X';
      this.gameOver = false;
    },
    getCellPosition(cellIndex) {
      const rowIndex = Math.floor(cellIndex / 3);
      const colIndex = cellIndex % 3;
      return [rowIndex, colIndex];
    }
  }
};
</script>

<style scoped>
.container1 {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
  background-size: cover;
  padding: 20px;
}

.board {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
  background-color: rgba(0, 0, 0, 0.8);
  margin-bottom: 12px;
}

.row {
  display: flex;
}

.cell {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 200px;
  height: 200px;
  background-color: #d8cfd0;
  border: 1px solid rgb(94, 1, 97);
  font-size: 36px;
  color:rgb(37, 37, 37);
  text-shadow: #00a2ff 1px 1px 2px;
  border-radius: 5px;
  
}

button {
  margin-top: 20px;
}

.button-tertiary {
  font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  padding: 10px 20px;
  margin: 4px 9px;
  font-size: 16px;
  border-radius: 4px;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  background-color: hsl(184, 93%, 89%);
  color: rgb(12, 12, 12);
  border-bottom-style: outset;
  border-right-style: ridge;
  border-left-style:outset;
  border-top-style:outset;
  font-size:large;
}

.button-tertiary:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.button-tertiary:hover {
  transform: translateY(-2px);
  box-shadow:  2px 4px 4px rgba(102, 46, 255, 0.952);
}

.button-tertiary:active {
  transform: translateY(0);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}
</style>
