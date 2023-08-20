<template>

    <!-- Main buttons -->

    <div class="tabs">
        <my-window>
        <h1>Main Buttons</h1>
        <div>
            <my-button @click="showPracticeTab = !showPracticeTab">Show/Hide Practice</my-button>
        </div>
        <div>
            <my-button @click="ReviewDialogVisible = !ReviewDialogVisible">Create Review</my-button>
            <my-button @click="showReviewsTab = !showReviewsTab">Show/hide reviews</my-button>
        </div>
        <div>
            <my-button @click="fetchPosts">Fetch posts</my-button>
            <my-button @click="showPostTab = !showPostTab">show\hide posts</my-button>
            <my-button v-if="posts.length" @click="PostDialogVisible = true">Create post</my-button>
        </div>
        </my-window>
    </div>
    
    <!-- Practice -->

    <div class="main">
    <my-window v-show="showPracticeTab">
        <div>
            <h2>Practice</h2>
            <img v-bind:src="defaultImage" width="320" height="180">
            <div> 
                <div v-for="image in images" 
                :key="image.imgId" 
                 @mouseover="updateImage(image.imgPath)"
                 class="color-circle"
                 :style="{backgroundColor: image.imgColor}"> 
            </div>
            </div>
            <autor-list :autors="autors">
            </autor-list>
            <my-button @click="addToBucket" :class="{disabledButton : outOfStock}">
                Add to bucket
            </my-button>
            <my-button>
                {{ bookCount }}
            </my-button>
            <h2 style="text-align: center;">Some useful links</h2>
        <div>
            <a :href="UrlHW" target="_blank">Java roadmap</a>
        </div>
        </div>
        
    </my-window>
    </div>

    <!-- Reviews -->

    <div class="reviews">
        

    <my-dialog v-model:show="ReviewDialogVisible">
        <review-form @review-submitted="addReview"></review-form>
    </my-dialog>
    
    <my-window v-show="showReviewsTab">
    <div  v-if="reviews.length">
        <review-list  :reviews="reviews"
        @removeReview="removeReview"></review-list>
    </div>
    <div v-else><h2>No reviews</h2></div>
    </my-window>
    
    
    </div>

    <!-- Posts -->

    <div class="posts">
    

    <my-dialog v-model:show="PostDialogVisible">
        <post-form 
        @post-submited="addPost"
        >
        </post-form>
    </my-dialog>
    
    <my-window  v-show="showPostTab">
        <post-list v-if="posts.length"
        :posts="posts" 
        @removePost="removePost">
        </post-list>
        <div v-else><h2>No Posts</h2></div>
    </my-window>
</div>
</template>

<script>

import AutorList from '@/components/Autors/AutorList'
import ReviewForm from '@/components/Reviews/ReviewForm'
import ReviewList from '@/components/Reviews/ReviewList'
import PostForm from '@/components/Posts/PostForm'
import PostList from '@/components/Posts/PostList'
import axios from 'axios'

    export default {
        components: {
            AutorList,ReviewForm,ReviewList,PostForm,PostList
        },
        data() {
            return {
                showPracticeTab: false,
                bookCount: 5,
                outOfStock: false,
                defaultImage: require('D:/desktop/VuePractice/vue-practice/src/assets/images/Open_book_nae_02.svg.png'),
                images: [
                    {imgId: 1, imgName: 'Book', imgColor:'green', imgPath: require('D:/desktop/VuePractice/vue-practice/src/assets/images/Open_book_nae_02.svg.png') },
                    {imgId: 2, imgName: 'Nothing', imgColor:'grey', imgPath: require('D:/desktop/VuePractice/vue-practice/src/assets/images/nothing.png')}
                ],
                UrlHW: 'https://drive.google.com/file/d/1NEsxE-9FCpxAty7GwW7MULgivZIQwlEA/view',
                autors: [
                    { id:1,
                    autorName: 'Franz Kafka',
                    bookName: 'Metamorphosis'
                },
                    { id:2,
                    autorName: 'Ernest Hemingway',
                    bookName: 'Old man and sea'
                }
                ],
                showReviewsTab: false,
                ReviewDialogVisible: false,
                reviews: [],
                posts: [],
                postsURL: "https://jsonplaceholder.typicode.com/posts?_limit=10",
                PostDialogVisible: false,
                showPostTab: false,

                
            }
        },
        mounted() {
        },
        methods: {
            updateImage(imageName) {
                this.defaultImage = imageName
            },

            addToBucket() {
                if(this.outOfStock) return
                if(this.bookCount === 1) {
                    this.bookCount--;
                    this.outOfStock = true
                    return
                }

                this.bookCount--;
                
            },

            addReview(review) {
                console.log(review);
                this.reviews.push(review);
                this.ReviewDialogVisible= false;
                this.showReviewsTab = true;
            },
            removeReview(review) {
                this.reviews = this.reviews.filter(p => p.id !== review.id)
            },

            async fetchPosts() {
                try {
                    const response = await axios.get(this.postsURL)
                    this.posts = response.data
                    console.log(this.posts);
                    this.showPostTab = true;
                    
                } catch(e){
                    alert("Ошибка")
                }

                // fetch(this.postsURL)
                //     .then(response => response.json())
                //     .then(data => this.posts = data)
                //     .catch(err => console.error(err))
                
            },
            addPost(post) {
                this.posts.push(post);
                console.log(this.posts);
                this.PostDialogVisible = false;
            },

            removePost(post) {
                this.posts = this.posts.filter(p => p.id !== post.id)
            },
            
        }
    }
</script>

<style>    
.color-circle {
    width: 50px;
    height: 50px;
    margin-top: 8px;
    border: 2px solid grey;
    border-radius: 50% ;
}

.disabledButton {
    cursor: not-allowed;
}
</style>