<template>
  <section class="quoridor">
    <h1 class="quoridor__title">QUORIDOR</h1>
    <p>Turno actual: {{ currentPlayer === 1 ? 'Jugador 1 (Rojo)' : 'Jugador 2 (Azul)' }}</p>
    <p v-if="winner">¡{{ winner }} ha ganado!</p>
    <board
      :board="board"
      :player1="player1"
      :player2="player2"
      :obstacles="obstacles"
      @cell-click="handleCellClick"
    />
    <br>
    <button @click="restart" class="quoridor__button">Reiniciar Juego</button>
    <footer class="quoridor__footer">
      <p>Realizado por<br>
      Cristian Javier Rodríguez Cárdenas <br>
      Frans Sebastian Villamizar Maldonado</p>
    </footer>
  </section>
</template>

<script>
import Board from './components/Board.vue';

export default {
  components: {
    Board
  },
  data() {
    return {
      board: this.createBoard(),
      player1: { x: 4, y: 0, color: 'red' },
      player2: { x: 4, y: 8, color: 'blue' },
      currentPlayer: 1, // Para alternar entre jugadores
      obstacles: [], // Array para almacenar la ubicación de los obstáculos
      winner: null // Para almacenar el ganador
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
      this.winner = null;
    },
    handleCellClick(i, j) {
      if (this.winner) return; // Si hay un ganador, no hacer nada

      const currentPlayer = this.currentPlayer === 1 ? this.player1 : this.player2;

      if (this.isValidMove(i, j)) {
        // Mover jugador
        currentPlayer.x = j;
        currentPlayer.y = i;
        this.checkForWinner();
        this.currentPlayer = this.currentPlayer === 1 ? 2 : 1; // Alternar entre jugadores
      } else if (!this.isPlayer1(i, j) && !this.isPlayer2(i, j) && !this.isObstacle(i, j)) {
        // Colocar un obstáculo si la celda está vacía y no contiene un jugador ni un obstáculo
        this.placeObstacle(i, j);
        this.currentPlayer = this.currentPlayer === 1 ? 2 : 1; // Alternar entre jugadores
      }
    },
    isValidMove(i, j) {
      const currentPlayer = this.currentPlayer === 1 ? this.player1 : this.player2;
      const dx = Math.abs(j - currentPlayer.x);
      const dy = Math.abs(i - currentPlayer.y);
      if ((dx === 1 && dy === 0) || (dx === 0 && dy === 1)) {
        return !this.isObstacle(i, j);
      }
      return false;
    },
    placeObstacle(i, j) {
      // Colocar un obstáculo en el tablero
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
    },
    checkForWinner() {
      if (this.player1.y === 8) {
        this.winner = 'Jugador 1 (Rojo)';
      } else if (this.player2.y === 0) {
        this.winner = 'Jugador 2 (Azul)';
      }
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