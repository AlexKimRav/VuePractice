<template>
    <div>
    <my-label>
        <div class="review">
        {{ review.name }} gave this {{ review.rating }} stars
                <br/>
                "{{review.review}}"

                <my-button @click="$emit('removeReview',review)">Delete</my-button>
            </div>
    </my-label>
    </div>
</template>

<script>
    export default {
        name: 'review-item',
        props: {
           review: {
            type: Object,
            required: true
        },
    }
}
</script>

<style scoped>
    .review {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>