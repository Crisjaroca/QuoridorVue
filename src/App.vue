<script>
export default {
  data() {
    return {
      board: this.createBoard(),
      player1: {x: 4, y: 0, color: 'red'},
      player2: {x: 4, y: 8, color: 'blue'},
    }
  },
  methods: {
    createBoard() {
      return Array(9).fill().map(() => Array(9).fill(null));
    },
    restart() {
      this.board = this.createBoard();
      this.player1 = {x: 4, y: 0, color: 'red'};
      this.player2 = {x: 4, y: 8, color: 'blue'};
    },
    isPlayer1(i, j) {
      return this.player1.x === j && this.player1.y === i;
    },
    isPlayer2(i, j) {
      return this.player2.x === j && this.player2.y === i;
    }
  }
}
</script>

<template>
  <section class="quoridor">
    <h1 class="quoridor__title">QUORIDOR</h1>
    <section class="quoridor__board">
      <section v-for="(row, i) in board" :key="i" class="quoridor__row">
        <section v-for="(cell, j) in row" :key="j" class="quoridor__cell">
          <section v-if="isPlayer1(i, j)" :style="{backgroundColor: player1.color}" class="quoridor__player"></section>
          <section v-if="isPlayer2(i, j)" :style="{backgroundColor: player2.color}" class="quoridor__player"></section>
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