<script>
export default {
  data() {
    return {
      tablero: this.crearTablero()
    }
  },
  methods: {
    crearTablero() {
      return Array(9).fill().map(() => Array(9).fill(null));
    }
  }
}
</script>

<template>
  <h1>Quoridor</h1>
  <section id="tablero">
    <section v-for="(fila, i) in tablero" :key="i" class="fila">
      <section v-for="(casilla, j) in fila" :key="j" class="casilla">
      </section>
    </section>
  </section>
  <footer>
    <p>Realizado por<br>
    Cristian Javier Rodríguez Cárdenas <br>
    Frans Sebastian Villamizar Maldonado</p>
  </footer>
</template>

<style scoped>
  h1 {
    text-align: center;
  }
  #tablero {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 20px;
  }
  .fila {
    display: flex;
  }
  .casilla {
    width: 50px;
    height: 50px;
    border: 1px solid black;
    position: relative;
  }
  footer {
    text-align: center;
    margin-top: 20px;
  }
</style>