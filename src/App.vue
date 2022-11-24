<template>
<header-menu/>
<div class="__container">
  <my-input 
     v-model="searchQuery" 
     placeholder="Поиск..."
     />

  <my-button style="margin: 15px 0 35px; background: teal; color: white;"
  @click="showDialog"
  >Создать пост</my-button>

  <my-select 
    v-model="selectedSort"
    :options="sortOptions"
  />



 
<my-dialog v-model:show="dialogVisible">
  <post-form 
  @create="createPost"
/>
</my-dialog>

<post-list 
  :posts = "sortedAndSearchedPosts"
  @remove="removePost"
  v-if="!isPostLoading"
/>
<div v-else>Идет загрузка...</div>
  
<div class="page__wrapper">
   <div 
      v-for="pageNumber in totalPages" 
      :key="pageNumber" 
      class="page" 
      :class="{
         'current-page': page === pageNumber
      }"
      @click="changePage(pageNumber)"
      > {{pageNumber}}
   </div>
</div>
  
</div>
</template>
 

<script>
import PostForm from './components/PostForm.vue';
import PostList from './components/PostList.vue';
import HeaderMenu from './components/HeaderMenu.vue';
import axios from 'axios';


export default {
   components: {
      PostForm, PostList, HeaderMenu,
   },
   data() {
      return {
         posts: [],
         dialogVisible: false,
         isPostLoading: false,
         selectedSort: '',
         page: 1,
         limit: 10,
         totalPages: 0,
         sortOptions: [
            {value: 'title', name: 'По названию' },
            {value: 'body', name: 'По содержанию' },
         ],
         searchQuery: '',
      }
   },
   methods: {
            createPost(post) {
               this.posts.push(post); 
               this.dialogVisible = false;
            },
            removePost (post){
                this.posts = this.posts.filter(p => p.id !== post.id)
            },
            showDialog(){
               this.dialogVisible = true;
            },

            async fetchPosts(){
               try{
                  this.isPostLoading = true;
                  const response = await axios.get('https://jsonplaceholder.typicode.com/posts', { 
                     params: {
                        _page: this.page,
                        _limit: this.limit,
                     }});
                     this.totalPages = Math.ceil(response.headers['x-total-count']/this.limit);
                  this.posts = response.data;
               }catch (e){
                  alert('Ошибка');
               } finally {
                  this.isPostLoading = false;
               }

            },
            changePage(pageNumber){
                 this.page = pageNumber;
                 this.fetchPosts();
            },
         },
         mounted(){
            this.fetchPosts();
         },
         computed: {
            sortedPosts(){
               return [...this.posts].sort( (post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
            },
            sortedAndSearchedPosts (){
               return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
            }

         },
         watch: {
           
            },
         
}
</script>
 

<style>
    @import url('https://fonts.googleapis.com/css2?family=Marko+One&family=Montserrat:wght@500;700;900&display=swap');

* {
   margin: 0;
   padding: 0;
   box-sizing: border-box;
   font-family: 'Marko One', serif;
   font-family: 'Montserrat', sans-serif;
}

ul, ul li {
	list-style: none;
}

a, a:link, a:visited  {
    text-decoration: none;
    display: inline-block;
}

a:hover  {
    text-decoration: none;
}

[class*="__container"] {
   max-width: 1150px;
   margin: 0px auto;
   padding: 0px 20px;
}

.page__wrapper{
   display: flex;
   margin: 1em auto;
   justify-content: center;
}

.page{
   border: 1px solid black;
   padding: 10px;
}

.current-page{
   border: 2px solid teal;
}

@media (max-width: 1150px) {
   [class*="__container"] {
      max-width: 970px;
   }
}

@media (max-width: 991.98px) {
   [class*="__container"] {
      max-width: 750px;
   }
}

@media (max-width: 767.98px) {
   [class*="__container"] {
      max-width: none;
   }
}
</style>