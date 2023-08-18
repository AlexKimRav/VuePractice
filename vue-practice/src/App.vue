<template>
    <my-label>
        <h2 style="text-align: center;">Полезные ссылки</h2>
        <div>
            <a :href="UrlHW" target="_blank">Java roadmap</a>
        </div>
        <br/>
        <my-button @click="isExist = !isExist">
            Показать\скрыть текст
        </my-button>
        <div v-if="isExist">
        <div>
            <h1>{{ product }}</h1>
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
                Добавить в корзину
            </my-button>
            <my-button>
                {{ bookCount }}
            </my-button>
        </div>
        
    </div>
    <div v-else><h1>Nothing here</h1></div>
</my-label>
    <my-label >
        <my-submit @review-submitted="addReview"></my-submit>
    </my-label>
    <my-label v-if="reviews.length">
        <review-list  :reviews="reviews"></review-list>
    </my-label>

    <my-button @click="fetchPosts">Получение постов</my-button>
    <my-label v-if="posts.length">
        <post-list :posts="posts">

        </post-list>
    
    </my-label>

</template>

<script>

import AutorList from '@/components/AutorList'
import MySubmit from '@/components/MySubmit'
import ReviewList from '@/components/ReviewList'
import PostList from '@/components/PostList'
import axios from 'axios'

    export default {
        components: {
            AutorList,MySubmit,ReviewList,PostList
        },
        data() {
            return {
                product: 'book',
                bookCount: 5,
                outOfStock: false,
                defaultImage: require('D:/desktop/VuePractice/vue-practice/src/assets/images/Open_book_nae_02.svg.png'),
                images: [
                    {imgId: 1, imgName: 'Book', imgColor:'green', imgPath: require('D:/desktop/VuePractice/vue-practice/src/assets/images/Open_book_nae_02.svg.png') },
                    {imgId: 2, imgName: 'Nothing', imgColor:'grey', imgPath: require('D:/desktop/VuePractice/vue-practice/src/assets/images/nothing.png')}
                ],
                UrlHW: 'https://drive.google.com/file/d/1NEsxE-9FCpxAty7GwW7MULgivZIQwlEA/view',
                isExist: false,
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
                reviews: [],
                posts: [],
                postsURL: "https://jsonplaceholder.typicode.com/posts?_limit=10",
                
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
            },

            async fetchPosts() {
                try {
                    const response = await axios.get(this.postsURL)
                    this.posts = response.data
                    console.log(this.posts);
                    
                } catch(e){
                    alert("Ошибка")
                }

                // fetch(this.postsURL)
                //     .then(response => response.json())
                //     .then(data => this.posts = data)
                //     .catch(err => console.error(err))
                
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