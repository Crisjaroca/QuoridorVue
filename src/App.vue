<script>
export default {
  data() {
    return {
      board: this.createBoard()
    }
  },
  methods: {
    createBoard() {
      return Array(9).fill().map(() => Array(9).fill(null));
    }
  }
}
</script>

<template>
  <section class="quoridor">
    <h1 class="quoridor__title">Quoridor</h1>
    <section class="quoridor__board">
      <section v-for="(row, i) in board" :key="i" class="quoridor__row">
        <section v-for="(cell, j) in row" :key="j" class="quoridor__cell">
        </section>
      </section>
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
  .quoridor__footer {
    margin-top: 20px;
  }
</style>