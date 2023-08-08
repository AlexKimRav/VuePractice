<template>
    <div>
        <h1>{{ product }}</h1>
        <h2>{{ description }}</h2>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                product: 'book',
                description: 'Just some book'
            }
        }
    }
</script>

<style >

</style>