<template>
    <div class="practice-label">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        name: 'my-label'
    }
</script>

<style scoped>
.practice-label {
    width: 50%;
    border: 15px solid teal;
    padding: 1em;
}
</style>