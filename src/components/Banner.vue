<template>
    <div id="main_banner">
        <h1><span>|</span>Make Your Burger</h1>
    </div>
</template>

<script>
export default {
    name: "Banner",
    data() {

    }
}
</script>

<style scoped>
    #main_banner{
        background: linear-gradient( rgba(0, 0, 0, .6), rgba(0, 0, 0, .6)), url('/img/burger.jpg');
        background-position: 0 -290px;
        background-size: cover;
        width: 100%;
        height: 500px;
        display: flex;
        justify-content: flex-start;
        align-items: center;
        border-radius: 10px;
        box-shadow: 0 0 10px 1px rgba( 0, 0, 0, .6);
    }

    #main_banner h1{
        color: #fff;
        margin-left: 1.5em;
        padding: .5em 1em;
        border-bottom: solid 6px #333;
        border-left: solid 6px #333;
        border-radius: 10px;
        box-shadow: 0 0 10px 1px rgba( 30, 30, 30, 1);
    }
</style>