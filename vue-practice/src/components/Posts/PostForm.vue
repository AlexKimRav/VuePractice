<template>
    <div>
        <form class="post-form" @submit.prevent="onSubmit">
            <h3>Создание поста</h3>
            <label for="title">Title:</label>
            <input class="input" id="title" v-model="title">

            <label for="body">Body:</label>
            <input class="input" id="body" v-model="body">

            <my-button type="submit" class="button">Submit</my-button>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'post-form',
        data() {
            return {
                title: '',
                body: '',
            }
        },
        methods: {
            onSubmit() {
                //validation
                    if(this.title === '' || this.body === '') {
                        alert("Please fill out every field")
                        return
                    }
                //obj
                    let objToSubmit = {
                        id: Date.now(),
                        title: this.title,
                        body: this.body
                    }

                //objToSend
                this.$emit('post-submited',objToSubmit)
                    
                //clean obj
                this.title = ''
                this.body = ''
            }
        }
    }
</script>

<style scoped>
.input {
    width: 100%;
    height: 4em;
    border: 3px solid teal;
}
.button {
    margin-top: 1em;
}
</style>