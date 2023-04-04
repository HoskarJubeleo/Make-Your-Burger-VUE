<template>
    <nav id="nav-bar">
        <RouterLink to="/" id="logo_url">
            <img :src="logo" :alt="alt" id="logo">
        </RouterLink>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/pedidos">Pedidos</RouterLink>
      </nav>
</template>

<script lang="ts">
    export default {
        name: "Navbar",

        props: ["logo", "alt"],

        data() {
            return {

            }
        }
    }
</script>

<style scoped> 
    #nav-bar{
        height: 10vh;
        padding: 1em 5em;
        display: flex;
        justify-content: flex-end;
        align-content: center;
        background: linear-gradient(#666, #222);
        border-bottom: solid 4px #111;
    }

    #nav-bar #logo_url{
        margin: auto;
        margin-left: 0;
    }

    #logo{
        width: 40px;
        height: 40px;
    }

    #nav-bar a{
        color: #FCBA03;
        text-decoration: none;
        margin: .8em;
        transition: .5s;
    }

    #nav-bar a:hover{
        color: #FFF;
    }
</style>