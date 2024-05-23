<template>
    <section :style="{ backgroundColor: color }" class="quoridor__player"></section>
</template>

<script>
export default {
    props: {
        color: String
    }
}
</script>

<style scoped>
.quoridor__player {
    position: absolute;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    top: 5px;
    left: 5px;
}
</style>