<template>
    <h3>Posts list</h3>
    <transition-group name="post-list">
        <post-item 
            v-for="post in posts"
            :post=post
            :key="post.id"
            @removePost="$emit('removePost', post)"
        />
    </transition-group>
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
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active, 
.post-list-leave-active {
  transition: all 0.2s ease;
}
.post-list-enter-from, 
.post-list-leave-to /* .list-leave-active до версии 2.1.8 */ {
  opacity: 0;
  transform: translateX(130px);
}
.post-list-move {
    transition: 0.2s ease;
}
</style>