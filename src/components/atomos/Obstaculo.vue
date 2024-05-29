<template>
    <article class="quoridor__obstacle"></article>
</template>

<script>
export default {}
</script>

<style scoped>
.quoridor__obstacle {
    width: 100%;
    height: 5px;
    background-color: rgb(119, 44, 0); /* Color del obstáculo*/
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
}
</style>