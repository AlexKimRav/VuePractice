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
    width: 60%;
    border: 15px solid teal;
    padding: 1em;
}
</style>