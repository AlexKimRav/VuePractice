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
                type: String,
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
    background-color: teal;
    color: white;
    border: 0.1rem solid black;
}

.select:hover {
    background-color: black;

}
</style>