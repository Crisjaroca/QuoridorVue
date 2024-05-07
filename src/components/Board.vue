    <template>
        <section class="board">
        <section v-for="(row, rowIndex) in board" :key="rowIndex" class="row">
            <section v-for="(cell, cellIndex) in row" :key="cellIndex" class="cell">
            <!-- Aquí podrías incluir otros componentes como Player y Obstacle según corresponda -->
            <Player 
                v-if="isPlayer(cell)" 
                :x="cell.x" 
                :y="cell.y" 
                :color="cell.color" 
                :cellSize="cellSize" 
                @click="movePlayer(cell)"
            />
            <Obstacle 
                v-if="isObstacle(cell)" 
                :x="cell.x" 
                :y="cell.y" 
                :cellSize="cellSize" 
            />
            </section>
        </section>
        </section>
    </template>
    
    <script>
    import Player from './Player.vue';
    import Obstacle from './Obstacle.vue';
    
    export default {
        components: {
        Player,
        Obstacle
        },
        props: {
        board: Array, // Pasar el tablero como una matriz de datos
        cellSize: Number // Tamaño de las celdas del tablero
        },
        methods: {
        isPlayer(cell) {
            // Función para verificar si la celda contiene un jugador
            // Implementar según tu lógica de datos
        },
        isObstacle(cell) {
            // Función para verificar si la celda contiene un obstáculo
            // Implementar según tu lógica de datos
        },
        movePlayer(position) {
            // Manejar el movimiento del jugador
            console.log('Move player to:', position);
            // Aquí puedes implementar la lógica para mover al jugador
        }
        }
    }
    </script>
    
    <style scoped>
    .board {
        display: flex;
        flex-direction: column;
        border: 2px solid #000;
        width: fit-content;
    }
    
    .row {
        display: flex;
    }
    
    .cell {
        width: 50px;
        height: 50px;
        border: 1px solid #000;
        position: relative;
    }
    </style>
    