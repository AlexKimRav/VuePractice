<template>
    <div>
        <h3>Reviews</h3>
        <ul>
            <my-label 
            v-for="review in reviews" 
            :key="review.id" 
            :post="post"
            >
                {{ review.name }} gave this {{ review.rating }} stars
                <br/>
                "{{review.review}}"
            </my-label>
        </ul>
    </div>
</template>

<script>
    export default {
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