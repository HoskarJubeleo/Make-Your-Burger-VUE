<template>
    <div class="alert alert-success" role="alert" id="msg">
        {{ msg }}
    </div>
</template>

<script lang="ts">
export default {
    name: "Message",
    props: {
        msg: String
    }
}
</script>

<style scoped>

</style>