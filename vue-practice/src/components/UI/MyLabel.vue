<template>
    <li class="li-list">
        <slot></slot>
    </li>
</template>

<script>
    export default {
        name: "my-label"
    }
</script>

<style scoped>
.li-list {
    margin: 5px;
    padding: 1em;
    border: 3px solid teal;
}
</style>