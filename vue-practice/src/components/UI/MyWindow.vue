<template>
    <div class="practice-window">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        name: 'my-window'
    }
</script>

<style scoped>
.practice-window {
    margin-top: 0.5em;
    margin-left: 0.5em;
    width: 60%;
    border: 15px solid teal;
    padding: 1em;
}
</style>