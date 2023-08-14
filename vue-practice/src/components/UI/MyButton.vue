<template>
        <button class="btn">
            <slot></slot>
        </button>
</template>

<script>
    export default {
        name: 'my-button'
    }
</script>

<style scoped>
.btn {
    padding: 1em;
    background-color: teal;
    color: white;
    width: auto;
    height: 3rem;
    border-radius: 5px;
}
</style>