<template>

<div class="app">
   <h3>Страница с постами</h3>
   <my-button 
   @click="showDialog"
   >Создать пост</my-button>
 <my-dialog v-model:show="dialogVisible">
   <post-form 
   @create="createPost"
 />
 </my-dialog>
 
 <post-list 
   :posts = "posts"
   @remove="removePost"
 />

</div>
 </template>
 

<script>
import PostForm from './components/PostForm.vue';
import PostList from './components/PostList.vue';

export default {
   components: {
      PostForm, PostList,
   },
   data() {
      return {
         posts: [
            { id: 1, title: 'Заголовок 1', body: 'Текст поста 1' },
            { id: 2, title: 'Заголовок 2', body: 'Текст поста 2' },
            { id: 3, title: 'Заголовок 3', body: 'Текст поста 3' },
         ],
         dialogVisible: false,
      }
   },
   methods: {
            createPost(post) {
               this.posts.push(post); 
            },
            removePost (post){
                this.posts = this.posts.filter(p => p.id !== post.id)
            },
            showDialog(){
               this.dialogVisible = true;
            }
            
         }
}
</script>
 

<style>
 * {
   margin: 0;
   padding: 0;
   box-sizing: border-box;
 }
 .app {
   padding: 20px;
 }


 </style>