<template>
    <h3>Список постов</h3>
    <post-item 
    v-for="post in posts"
    :post=post
    :key="post.id"
    @remove="$emit('remove', post)"
    >
    </post-item>
</template>

<script>
import PostItem from '@/components/Posts/PostItem';
    export default {
        components: {PostItem},
        name: "post-list",
        props: {
            posts: {
                type: Array,
                required: true
            }
        }
    }
</script>

<style scoped>

</style>