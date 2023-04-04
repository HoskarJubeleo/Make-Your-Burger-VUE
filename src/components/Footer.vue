<template>
    <footer>
        <p>Make Your Burger &copy; 2023 </p>
    </footer>
</template>

<script lang="ts">
export default {
    name: "Footer",
    data() {
        return {

        }
    }
}
</script>

<style scoped>
    footer{
        width: 100%;
        height: 10vh;
        background: #222;
        border-top: solid 4px #111;
        color: #FCBA03;
        display: flex;
        align-content: center;
        justify-content: center;
        bottom: 0;
    }
</style>