<template>

    <!-- Main buttons -->

    <div class="tabs">
        <my-window>
        <h1>Main Buttons</h1>
        <div>
            <my-button @click="showPracticeTab = !showPracticeTab">Show/Hide Practice</my-button>
        </div>
        <div>
            <my-button @click="showReviewsTab = !showReviewsTab">Show/hide reviews</my-button>
        </div>
        <div>
            <my-button @click="fetchPosts">Fetch posts</my-button>
            <my-button @click="showPostTab = !showPostTab">show\hide posts</my-button>
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
        <div v-for="item in UrlHW">
            <a :href="item.url" target="_blank">{{ item.name }} roadmap</a>
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
        <div class="dialog-nav">
        <my-button @click="ReviewDialogVisible = !ReviewDialogVisible">Create Review</my-button>
        <my-select 
            v-model="selectedSortReview"
            :options="reviewSortOptions">
            </my-select>
        </div>
        <my-input v-model="searchQueryReview" placeholder="search by name"/>

    <div  v-if="reviews.length">
        <review-list  :reviews="sortedAndSearchedReviews"
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
        <div class="dialog-nav">
            <my-button  @click="PostDialogVisible = true">Create post</my-button>
            <my-select 
            v-model="selectedSortPost"
            :options="postSortOptions">
            </my-select>
        </div>
        <my-input v-model="searchQueryPost" placeholder="search by title"/>
        <post-list v-if="posts.length"
        :posts="sortedAndSearchedPosts" 
        @removePost="removePost">
        </post-list>
        <div v-else><h2>No Posts</h2></div>
    </my-window>
</div>

<div ref="observer" class="observer"></div>
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
            AutorList,ReviewForm,ReviewList,PostForm,PostList,
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
                UrlHW: [
                {name:'Java', url: 'https://drive.google.com/file/d/1NEsxE-9FCpxAty7GwW7MULgivZIQwlEA/view'},
                {name:'Js', url: 'https://roadmap.sh/javascript'},
                {name:'Vue', url: 'https://roadmap.sh/vue'},
                ],
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
                selectedSortPost: '',
                selectedSortReview: '',
                postSortOptions: [
                    {value: 'title', name: 'By title'},
                    {value: 'body', name: 'By description'},
                    {value: 'id', name: 'By id'}
                ],
                reviewSortOptions: [
                    {value: 'id', name: 'By Id'},
                    {value: 'name', name: 'By Name'},
                    {value: 'review', name: 'By Review'},
                    {value: 'rating', name: 'By Rating'},

                ],
                searchQueryPost: '',
                searchQueryReview: ''
                
            }
        },
        mounted() {
            const options = {
                rootMargin: '0px',
                threshold: 1.0
            }
            
            const callback = function(entries,observer) {
                if (entries[0].isIntersecting) {
                    console.log('Пересечен');
                }
            }
            const observer = new IntersectionObserver(callback,options);
            observer.observe(this.$refs.observer)
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
                    console.log(e);
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
        },
        computed: {
            sortedReviews() {
                if(this.selectedSortReview === 'id') {
                    return this.reviews.sort((a, b) => {
                        if (a.id < b.id) return -1;
                        if (a.id > b.id) return 1;
                        return 0;
                }) 
            }
                else if (this.selectedSortReview === 'rating') {
                    return this.reviews.sort((a, b) => {
                        if (a.rating < b.rating) return -1;
                        if (a.rating > b.rating) return 1;
                        return 0;
                })          
                }

                return [...this.reviews].sort((review1,review2) => review1[this.selectedSortReview]?.localeCompare(review2[this.selectedSortReview]))
            },
            
            sortedAndSearchedReviews() {
                return this.sortedReviews.filter(review => review.name.toLowerCase().includes(this.searchQueryReview.toLowerCase()))
            },

            
            sortedPosts() {
                if(this.selectedSortPost === 'id') {
                    return this.posts.sort((a, b) => {
                        if (a.id < b.id) return -1;
                        if (a.id > b.id) return 1;
                        return 0;
                })
            }
                return [...this.posts].sort((post1,post2) => post1[this.selectedSortPost]?.localeCompare(post2[this.selectedSortPost]))
            },
            sortedAndSearchedPosts() {
                return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQueryPost.toLowerCase()))
            }
        }
    }
</script>

<style>    
* {
    margin: 0;
    padding: 0;
    list-style-type: none;

}
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

.dialog-nav {
    display: flex; 
    justify-content: space-between;
}

.observer {
    height: 10em;
    background-color: rgb(1, 10, 64);
}
</style>