<template>
    <div>
        <form class="review-form" @submit.prevent="onSubmit">
            <h3>Leave a review</h3>
            <label for="name">Name:</label>
            <input class="input" id="name" v-model="name">

            <label for="review">Review:</label>
            <input class="input" id="review" v-model="review">

            <label for="rating">Rating:</label>
            <select class="input" id="rating" v-model.number="rating">
                <option>5</option>
                <option>4</option>
                <option>3</option>
                <option>2</option>
                <option>1</option>
            </select>
            <!-- <input class="button" type="submit" value="Submit"> -->
            <my-button type="submit" class="button">Submit</my-button>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'my-submit',
        data() {
            return {
                name: '',
                review: '',
                rating: null
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
.input {
    width: 100%;
    height: 4em;
    border: 3px solid teal;
}
.review-form  label {
    display: block;
    margin-top: 1em;
}

.button {
    display: block;
    margin-top: 1em;
  
}
</style>