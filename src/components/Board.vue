<template>
    <section class="quoridor__board">
        <section v-for="(row, i) in board" :key="i" class="quoridor__row">
            <section v-for="(cell, j) in row" :key="j" class="quoridor__cell" @click="handleClick(i, j)">
                <player v-if="isPlayer1(i, j)" :color="player1.color" />
                <player v-if="isPlayer2(i, j)" :color="player2.color" />
                <obstacle v-if="isObstacle(i, j)" />
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
        board: Array,
        player1: Object,
        player2: Object,
        obstacles: Array
    },
    methods: {
        handleClick(i, j) {
            this.$emit('cell-click', i, j);
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
</style>