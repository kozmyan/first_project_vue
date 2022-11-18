<template>

   <div 
   class="dialog" 
   v-if="show" 
   @click.stop="hideDialog"
   >
    <div class="dialog__content" @click.stop>
        <h3>Создание поста</h3>
        <slot></slot>
    </div>

   </div>
</template>
   
   
   
   <script>
  
   export default {
      name: 'my-dialog',
      props: {
        show: {
            type: Boolean,
            default: false
        }
      },
      methods:{
        hideDialog (){
            this.$emit('update:show', false)
        }
      }
   }
   </script>
   
   <style scoped>
       .dialog {
          top: 0;
          left: 0;
          right: 0;
          bottom: 0;
          background: rgb(0, 0, 0, 0.5);
          position: fixed;
       }

       .dialog__content {
         margin: 100px auto;
         background: white;
         border-radius: 10px;
         min-height: 50px;
         max-width: 500px;
         padding: 15px;
       }

   </style>