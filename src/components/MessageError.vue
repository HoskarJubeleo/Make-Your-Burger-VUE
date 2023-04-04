<template>
    <div class="alert alert-danger" role="alert">
        {{ msg }}
    </div>
</template>

<script lang="ts">
export default {
    name: "MessageError",
    props: {
        msg: String
    }
}
</script>

<style scoped>

</style>