<template>

    <!-- Практика -->

    <my-window>
        
        <br/>
        <my-button @click="isExistFirstLabel = !isExistFirstLabel">
            Показать\скрыть текст
        </my-button>
        <div v-if="isExistFirstLabel">
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
            <h2 style="text-align: center;">Полезные ссылки</h2>
        <div>
            <a :href="UrlHW" target="_blank">Java roadmap</a>
        </div>
        </div>
        
    </div>
    <div v-else><h1>Nothing here</h1></div>
    </my-window>

    <!-- Ревью -->

    <my-window >
        <review-form @review-submitted="addReview"></review-form>
    </my-window>


    <my-window v-if="reviews.length">
        <review-list  :reviews="reviews"></review-list>
    </my-window>

    <!-- Посты -->
    <my-button @click="fetchPosts">Получение постов</my-button>
    
    <my-button>
        Создать пост
    </my-button>
    
    <my-button  v-if="posts.length"
    @click="isExistSecondLabel = !isExistSecondLabel"
    >Показать\скрыть посты
    </my-button>

    <my-dialog v-model:show="PostDialogVisible">

    </my-dialog>
    
    <my-window v-if="posts.length" v-show="isExistSecondLabel">
        <post-list 
        :posts="posts" 
        @remove="removePost">

        </post-list>
    </my-window>

</template>

<script>

import AutorList from '@/components/Autors/AutorList'
import ReviewForm from '@/components/Reviews/ReviewForm'
import ReviewList from '@/components/Reviews/ReviewList'
import PostList from '@/components/Posts/PostList'
import axios from 'axios'

    export default {
        components: {
            AutorList,ReviewForm,ReviewList,PostList
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
                isExistFirstLabel: false,
                isExistSecondLabel: true,
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
                PostDialogVisible: false
                
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