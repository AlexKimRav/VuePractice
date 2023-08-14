<template>
    <div>
        <my-button @click="showText">
            Показать\скрыть текст
        </my-button>
        <div v-if="isExist">
        <div>
            <h1>{{ product }}</h1>
            <h2>{{ description }}</h2>
            <div class="image-file"> 
                <img v-bind:src="image" width="480" height="320">
            </div>
            <autor-list :autors="autors">
            </autor-list>
        </div>
        <h2 style="text-align: center;">Полезные ссылки</h2>
        <div>
            <a :href="UrlHW" target="_blank">Java roadmap</a>
        </div>
    </div>
    <div v-else><h1>Nothing here</h1></div>
    </div>
</template>

<script>

import AutorList from '@/components/AutorList'

    export default {
        components: {
            AutorList
        },
        data() {
            return {
                product: 'book',
                description: 'Just some book',
                image: require('D:/desktop/VuePractice/vue-practice/src/assets/images/Open_book_nae_02.svg.png'),
                UrlHW: 'https://drive.google.com/file/d/1NEsxE-9FCpxAty7GwW7MULgivZIQwlEA/view',
                isExist: false,
                autors: [
                    {id:1,
                    autorName: 'Franz Kafka',
                    bookName: 'Metamorphosis'
                },
                    {id:2,
                    autorName: 'Ernest Hemingway',
                    bookName: 'Old man and sea'
                }
                ],
                
            }
        },
        mounted() {
            this.showText()
        },
        methods: {
            showText() {
                setTimeout(() => {
                    this.isExist = this.isExist ? false : true
                    return this.isExist
                }, 2000)
                
            }
        }
    }
</script>

<style >

</style>