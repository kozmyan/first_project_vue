<template>
  <div>
    <form @submit.prevent>
      <input 
      v-model="post.title" 
      class="input" 
      type="text" 
      placeholder="Название">

      <input 
      v-model="post.body" 
      class="input" 
      type="text" 
      placeholder="Описание">

      <button 
      @click="createPost" 
      class="btn">Создать
      </button>
    </form>

  </div>
</template>



<script>

export default {

  data() {
    return {
       post: {
        title: '',
        body: '',
       }
    }
  },
  methods: {

  }
}
</script>




<style scoped>
.input{
   width: 100%;
   border: 2px solid teal;
   margin-top: 15px;
   padding: 15px;
 }

 form{
   display: flex;
   flex-direction: column;
 }

 .btn{
   border: 2px solid teal;
   color: teal;
   width: 150px;
   height: 40px;
   margin-top: 15px;
   align-self: flex-end;
 }
</style>