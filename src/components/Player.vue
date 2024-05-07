    <template>
        <section 
        class="player" 
        :style="{ backgroundColor: color, top: y * cellSize + 'px', left: x * cellSize + 'px' }"
        @click="handleClick"
        ></section>
    </template>
    
    <script>
    export default {
        props: {
        x: {
            type: Number,
            required: true
        },
        y: {
            type: Number,
            required: true
        },
        color: {
            type: String,
            required: true
        },
        cellSize: {
            type: Number,
            required: true
        }
        },
        methods: {
        handleClick() {
            // Emitir un evento de clic con la posición del jugador cuando se haga clic en la ficha
            this.$emit('click', { x: this.x, y: this.y });
        }
        }
    }
    </script>
    
    <style scoped>
    .player {
        position: absolute;
        width: 40px;
        height: 40px;
        border-radius: 50%;
    }
    </style>
        