<template>
<div>
    <my-label class = "post">
        <div>
            <div><strong>Id:</strong> {{ post.id }}</div> <!-- TODO Позже убрать -->            
            <div><strong>Название:</strong> {{ post.title }}</div>
            <div><strong>Описание:</strong> {{ post.body }}</div>
        </div>
            <my-button
                @click="$emit('removePost', post)"
                >Удалить
            </my-button>
    </my-label>
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
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>