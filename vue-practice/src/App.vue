<template>
    <div class="practice-label">
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
            <my-button @click="AddToBucket" :class="{disabledButton : outOfStock}">
                Добавить в корзину
            </my-button>
            <my-button>
                {{ bookCount }}
            </my-button>
        </div>
        
    </div>
    <div v-else><h1>Nothing here</h1></div>
    </div>
    <div class="practice-label">
        <my-submit @review-submitted="addReview"></my-submit>
    </div>
    <div v-if="reviews.length" class="practice-label">
        <review-list  :reviews="reviews"></review-list>
    </div>

</template>

<script>

import AutorList from '@/components/AutorList'
import MySubmit from '@/components/MySubmit'
import ReviewList from '@/components/ReviewList'

    export default {
        components: {
            AutorList,MySubmit,ReviewList
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
                
            }
        },
        mounted() {
        },
        methods: {
            updateImage(imageName) {
                this.defaultImage = imageName
            },

            AddToBucket() {
                if(this.outOfStock) return
                if(this.bookCount === 1) {
                    this.bookCount--;
                    this.outOfStock = true
                    return
                }

                this.bookCount--;
                
            },

            addReview(review) {
                this.reviews.push(review);
                console.log(this.reviews);
            }
            
        }
    }
</script>

<style>    
.practice-label {
    width: 50%;
    border: 15px solid teal;
    padding: 1em;
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
</style>