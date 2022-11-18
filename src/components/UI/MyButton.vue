<template>
   <button class="btn">
    <slot></slot>
   </button>
</template>
 
 
 
 <script>

 export default {
   
    name: 'my-button'
 }
 </script>
 
 <style scoped>
   .btn{
   border: 2px solid teal;
   color: teal;
   width: 120px;
   height: 30px;
   align-self: flex-end;
 }
 </style>