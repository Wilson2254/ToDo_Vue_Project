<template lang="html">
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title">
    <button type="submit">Add</button>
  </form>
</template>

<script>
export default {
  data(){
    return{
      title:''
    }
  },
  methods:{
    onSubmit(){
      if(this.title.trim()){
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false
        }
        this.$emit('add-todo', newTodo)
        this.title = ''
      }
    }
  }
}
</script>

<style lang="css" scoped>
  form{
    display: flex;
    justify-content: center;
  }

  button{
    background-color: gray;
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 20px;
    margin: 8px 5px;
    border-radius: 4px;
    cursor: pointer;
    font-family: 'Odibee Sans';
  }

  input[type=text] {
    width: 80%;
    padding: 12px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    font-family: 'Odibee Sans';
    font-size: 20px;
  }
</style>
