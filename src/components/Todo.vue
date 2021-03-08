<template>
  <div>
  <form @submit.prevent="addTodo">
    <transition name="lists">
    <div v-if="error" class="error alert">{{error}}</div>
    </transition>
    <input type="text" v-model="todo">
    <br>
    <input type="submit" value="Add To Do">
  </form>
  
    <div>
    <transition-group tag="ul" name="lists">
      <li>basketabll</li>
      <li v-for="todoitem in todolist" :key="todoitem" @click.self="removeItem">{{todoitem}}</li>
    </transition-group>
    </div>
    
  </div>
</template>

<script>
  export default {
    data(){
      return{
        todo: '',
        todolist: [],
        error: ''
      }
    },
    methods:{
      addTodo(){
        if(!this.todo){
          this.error = 'Empty Field '
        }
        else{
        this.error = ''
        this.todolist.push(this.todo)
        this.todo = ''
        }
      },
      
      removeItem(e){
        e.target.remove()
        this.error = ''
      }
    }
    
  }
</script>

<style>
*{
  padding: 0;
  margin: 0;
}
  form{
    text-align: center;
    padding: 5px;
  }
  input[type="text"]{
    font-size: 1rem;
    border: none;
    border-bottom: 2px solid black;
    outline: none;
    padding: 2px;
  }
  input[type="submit"]{
    margin-top: 10px;
    font-size: 1rem;
    border-radius: 10px;
    border: 1px solid gray;
    background: #f5f5f5;
    padding: 10px 20px;
    outline: none;
  }
  input[type="submit"]:hover{
    background-color: #f1f1f1;
    cursor: pointer;
  }
  .error{
    padding: 15px 20px;
    margin: 5px 0;
    background-color: crimson;
    color: white;
    border-radius: 10px
  }
  li{
    list-style: none;
    padding: 20px 50px;
    border: 1px solid gray;
    border-radius: 20px;
    margin: 10px 40px 10px 40px;
  
    
  }
  .lists-enter-from{
    opacity: 0;
    transform: scale(.6);
  }
  .lists-enter-to{
    opacity: 1;
    transform: scale(1);
  }
  .lists-leave-from{
    opacity: 1;
    transform: scale(1);
  }
  .lists-leave-to{
    opacity: .5;
    transform: scale(.6);
  }
  
  .lists-enter-active, .lists-leave-active{
    transition: all .5s ease;
    /*animation: ladder .5s ease;*/
  }
  
  @keyframes ladder{
    0%{
      opacity: 0;
      transform: translateY(-60px);
    }
    50%{
      opacity: 1;
      transform: translateY(0);
      transform: scale(.2);
    }
  
    80%{
      transform: scale(.6);
    }
    90%{
      transform: scale(.8);
    }
    100%{
      transform: scale(1);
    }
  }
</style>