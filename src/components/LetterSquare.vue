<template>
    <div class="letterSquare">
        <p>{{ letter }}</p>
    </div>
</template>

<script>
export default {
    props: {
        letter: String,
    },
};
</script>

<style scoped>
.letterSquare {
    width: 3em;
    height: 3em;
    background-color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
    border-radius: 0.3em;
    text-transform: uppercase;
    font-weight: bold;
    font-size: larger;
}
</style>
