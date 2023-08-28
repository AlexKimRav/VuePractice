<template>
        <select class="select" :value="modelValue" @change="changeOption">
            <option disabled value="">Choose the option</option>
            <option v-for="option in options" 
            :key=option.value
            :value="option.value"
            >
            {{ option.name }}
            </option>
        </select>
</template>

<script>
    export default {
         name: 'my-select',
         props: {
            modelValue: {
                type: [String,Number],
            },
            options: {
                type: Array,
                default: () => [] //дефолтный пустой массив
            },
         },
         methods: {
            changeOption(event) {
                this.$emit('update:modelValue', event.target.value)
            }
         }
    }
</script>

<style scoped>
.select {
    height: 3rem;
    border: 0.2rem solid teal;
}
</style>