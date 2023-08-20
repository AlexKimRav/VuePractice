<template>
    <div>
        <h3>Reviews</h3>
        <ul>
            <review-item
                v-for="review in reviews" 
                :key="review.id"
                :review="review"
                @removeReview="$emit('removeReview',review)">
            </review-item>
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

</style>