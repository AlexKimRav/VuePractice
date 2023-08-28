<template>
    <div>
        <form class="review-form" @submit.prevent="onSubmit">
            <h3>Leave a review</h3>
            <label for="name">Name:</label>
            <my-input  id="name" v-model="name"/>

            <label for="review">Review:</label>
            <my-input id="review" v-model="review"/>

            <label for="rating">Rating:</label>
            <my-select class="input" id="rating" v-model.number="rating" :options="options">
            </my-select>
            <!-- <input class="button" type="submit" value="Submit"> -->
            <my-button type="submit" class="button">Submit</my-button>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'review-form',
        data() {
            return {
                name: '',
                review: '',
                rating: null,
                options: [
                {name: 'one star', value: 1},
                {name: 'two stars', value: 2},
                {name: 'three stars', value: 3},
                {name: 'four stars', value: 4},
                {name: 'five stars', value: 5}
                ]
            }
        },
        methods: {
            onSubmit() {
                if (this.name === '' || this.review === '' || this.rating === null || this.rating < 1 || this.rating > 5) {
                    alert('Review is incomplete. Please fill out every field.')
                    return
                }

                


                let productReview= {
                    id: Date.now(),
                    name: this.name,
                    review: this.review,
                    rating: this.rating
                }

                this.$emit('review-submitted', productReview)
                this.id = null;
                this.name='';
                this.review='';
                this.rating=null;
            }
        }
    }
</script>

<style scoped>
.review-form  label {
    display: block;
    margin-top: 1em;
}

.button {
    display: block;
    margin-top: 1em;
  
}
</style>