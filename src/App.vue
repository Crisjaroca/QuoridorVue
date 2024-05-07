<template>
  <section class="quoridor">
    <h1 class="quoridor__title">QUORIDOR</h1>
    <section class="quoridor__board">
      <section v-for="(row, i) in board" :key="i" class="quoridor__row">
        <section v-for="(cell, j) in row" :key="j" class="quoridor__cell" @click="handleCellClick(i, j)">
          <section v-if="isPlayer1(i, j)" :style="{backgroundColor: player1.color}" class="quoridor__player"></section>
          <section v-if="isPlayer2(i, j)" :style="{backgroundColor: player2.color}" class="quoridor__player"></section>
          <section v-if="isObstacle(i, j)" class="quoridor__obstacle"></section>
        </section>
      </section>
      <br>
      <button @click="restart" class="quoridor__button">Restart Game</button>
    </section>
    <footer class="quoridor__footer">
      <p>Realizado por<br>
      Cristian Javier Rodríguez Cárdenas <br>
      Frans Sebastian Villamizar Maldonado</p>
    </footer>
  </section>
</template>

<script>
export default {
  data() {
    return {
      board: this.createBoard(),
      player1: { x: 4, y: 0, color: 'red' },
      player2: { x: 4, y: 8, color: 'blue' },
      currentPlayer: 1, // Para alternar entre jugadores
      obstacles: [] // Array para almacenar la ubicación de los obstáculos
    }
  },
  methods: {
    createBoard() {
      return Array(9).fill().map(() => Array(9).fill(null));
    },
    restart() {
      this.board = this.createBoard();
      this.player1 = { x: 4, y: 0, color: 'red' };
      this.player2 = { x: 4, y: 8, color: 'blue' };
      this.currentPlayer = 1; // Restablecer al jugador 1 como el jugador actual
      this.obstacles = [];
    },
    handleCellClick(i, j) {
      if (this.currentPlayer === 1 && this.isPlayer1(i, j)) {
        // Permitir al jugador 1 moverse
        this.movePlayer(i, j);
      } else if (this.currentPlayer === 2 && this.isPlayer2(i, j)) {
        // Permitir al jugador 2 moverse
        this.movePlayer(i, j);
      } else if (!this.isPlayer1(i, j) && !this.isPlayer2(i, j) && !this.isObstacle(i, j)) {
        // Colocar un obstáculo si la celda está vacía y no contiene un jugador ni un obstáculo
        this.placeObstacle(i, j);
      }
    },
    movePlayer(i, j) {
      if (this.isValidMove(i, j)) {
        if (this.currentPlayer === 1) {
          this.player1.x = j;
          this.player1.y = i;
        } else {
          this.player2.x = j;
          this.player2.y = i;
        }
        this.currentPlayer = this.currentPlayer === 1 ? 2 : 1; // Alternar entre jugadores
      }
    },
    isValidMove(i, j) {
      // Verificar si la celda a la que el jugador intenta moverse está adyacente a su posición actual
      const dx = Math.abs(j - (this.currentPlayer === 1 ? this.player1.x : this.player2.x));
      const dy = Math.abs(i - (this.currentPlayer === 1 ? this.player1.y : this.player2.y));
      if ((dx === 1 && dy === 0) || (dx === 0 && dy === 1)) {
        // Verificar si la celda está vacía o si está ocupada por otro jugador
        if (!this.isPlayer1(i, j) && !this.isPlayer2(i, j) && !this.isObstacle(i, j)) {
          return true;
        }
      }
      return false;
    },
    placeObstacle(i, j) {
      // Lógica para colocar obstáculos en el tablero
      // Implementar aquí la lógica para que los jugadores puedan colocar obstáculos
      this.obstacles.push({ x: j, y: i });
    },
    isPlayer1(i, j) {
      return this.player1.x === j && this.player1.y === i;
    },
    isPlayer2(i, j) {
      return this.player2.x === j && this.player2.y === i;
    },
    isObstacle(i, j) {
      return this.obstacles.some(obstacle => obstacle.x === j && obstacle.y === i);
    }
  }
}
</script>

<style scoped>
.quoridor {
  text-align: center;
}

.quoridor__title {
  margin-bottom: 20px;
}

.quoridor__board {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

.quoridor__row {
  display: flex;
}

.quoridor__cell {
  width: 50px;
  height: 50px;
  border: 1px solid black;
  position: relative;
}

.quoridor__player {
  position: absolute;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  top: 5px;
  left: 5px;
}

.quoridor__obstacle {
  position: absolute;
  width: 50px;
  height: 5px;
  background-color: brown;
}

.quoridor__button {
  display: block;
  margin: 0 auto;
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}

.quoridor__button:hover {
  background-color: #45a049;
}

.quoridor__footer {
  margin-top: 20px;
}
</style>
