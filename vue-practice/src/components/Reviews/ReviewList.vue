<template>
    <div>
        <h3>Reviews</h3>
        <ul>
            <transition-group name="review-list">
            <review-item
                v-for="review in reviews" 
                :key="review.id"
                :review="review"
                @removeReview="$emit('removeReview',review)">
            </review-item>
        </transition-group>
        </ul>
    </div>
</template>

<script>
import ReviewItem from '@/components/Reviews/ReviewItem';

    export default {
        components: {
            ReviewItem
        },
        name: "review-list",
        props: {
            reviews: {
                type: Array,
                required: true
            }
        }
    }
</script>

<style scoped>
.review-list-item {
  display: inline-block;
  margin-right: 10px;
}
.review-list-enter-active, 
.review-list-leave-active {
  transition: all 0.2s ease;
}
.review-list-enter-from, 
.review-list-leave-to /* .list-leave-active до версии 2.1.8 */ {
  opacity: 0;
  transform: translateX(130px);
}
.review-list-move {
    transition: 0.2s ease;
}
</style>