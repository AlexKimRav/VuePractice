!<template>
    <div>
        <ul>
            <li v-for="autor in autors" :key="autor.id" :value="autor.autorName"> {{ autor.autorName }} : "{{ autor.bookName }}"</li>
        </ul>
    </div>
</template>

<script>
    export default {
        props: {
            autors: {
                type: Array,
                required: true
            }
        }
    }
</script>

<style scoped>

</style>