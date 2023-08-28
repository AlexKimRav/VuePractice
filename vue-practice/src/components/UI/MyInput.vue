<template>
    <input :value="modelValue" @input="updateInput" class="input" type="text">
</template>

<script>
    export default {
        name: 'my-input',
        props: {
            modelValue: [String,Number]
        },
        methods: {
            updateInput(event) {
                this.$emit('update:modelValue',event.target.value)
            }
        }
    }
</script>

<style scoped>
.input {
    width: 100%;
    height: 4em;
    border: 3px solid teal;
    margin-top: 1em;
}
</style>