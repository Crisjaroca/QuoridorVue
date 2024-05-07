    <template>
        <section class="obstacle" :style="{ top: y * cellSize + 'px', left: x * cellSize + 'px' }"></section>
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
        cellSize: {
            type: Number,
            required: true
        }
        }
    }
    </script>
    
    <style scoped>
    .obstacle {
        position: absolute;
        width: 50px;
        height: 5px;
        background-color: brown;
    }
    </style>
    