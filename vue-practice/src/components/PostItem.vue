<template>
<div>
    <div class = "post">
        <div>
            <div><strong>Id:</strong> {{ post.id }}</div> <!-- TODO Позже убрать -->            
            <div><strong>Название:</strong> {{ post.title }}</div>
            <div><strong>Описание:</strong> {{ post.body }}</div>
        </div>
        <div class="post__btns">
            <my-button
                @click="$emit('remove', post)"
                >Удалить
            </my-button>
        </div>
    </div>
</div>        
</template>

<script>
    export default {
        name: "post-item",
        props: {
            post: {
                type: Object,
                required: true
            }
        }
    }
</script>

<style scoped>
.post {
    margin-top: 1em;
    padding: 1em;
    border: 3px solid teal;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>