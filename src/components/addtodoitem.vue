<template>
   <form v-on:submit.prevent="onSubmit">
      <input type="text" v-model="title">
      <button type="submit">Добавить в список</button> 
   </form>
</template>
<script>  
 
export default {
   data(){
      return {
         title: ''
      }
   },
   methods:{
      onSubmit(){
         console.log('submit')
         console.log(this.title)
         if(this.title.trim()){
            const newTodo ={
               id: Date.now(),
               title: this.title,
               completed: false,
            }
            this.$emit('new-todo', newTodo)
            this.title = ''
         }
      },
   }
}
</script>
