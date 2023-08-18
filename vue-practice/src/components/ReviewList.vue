<template>
    <div>
        <h3>Reviews</h3>
        <ul>
            <li v-for="review in reviews" :key="review.id" class="li-list">
                {{ review.name }} gave this {{ review.rating }} stars
                <br/>
                "{{review.review}}"
            </li>
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
.li-list{
    margin: 5px;
    padding: 1em;
    border: 3px solid teal;
}
</style>