<template>
    <div>
        <form class="post-form" @submit.prevent="onSubmit">
            <h3>Create post</h3>
            <my-input   v-model="title" placeholder="Title"/>
            <my-input  v-model="body" placeholder="Description"/>

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
.button {
    margin-top: 1em;
}
</style>