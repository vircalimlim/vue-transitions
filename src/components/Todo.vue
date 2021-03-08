<template>
  <form @submit.prevent="addTodo">
    
    <transition name="alert">
    <div v-if="error" class="error alert"><p>{{error}}</p></div>
    </transition>
    
    <input type="text" v-model="todo">
    <br>
    <input type="submit" value="Add To Do">
    <div v-for="todoitem in todolist">
      <p @click.self="removeItem">{{todoitem}}</p>
    </div>
  </form>
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

<style >
/* do not use scoped when doing animations it won't work*/
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
    padding: 5px 20px;
    margin: 5px 0;
    background-color: crimson;
    color: white;
    border-radius: 10px
  }
  
  
  
 /* .alert-enter-from{
    opacity: 0;
    transform: translateX(-60px);
  }
  .alert-enter-to{
    opacity: 1;
    transform: translateX(0);
  }*/
  
  .alert-enter-active{
   /* transition: all 1s ease; */
    animation: wobbleIn 0.5s ease;
  }
  .alert-leave-active{
    animation: wobbleOut 0.5s ease;
  }
  
  @keyframes wobbleIn {
    0% { transform: translateY(-60px); opacity: 0 }
    50% { transform: translateY(0); opacity: 1 }
    60% { transform: translateX(8px) }
    70% { transform: translateX(-8px) }
    80% { transform: translateX(4px) }
    90% { transform: translateX(-4px) }
    100% { transform: translateX(0) }
  }
  

  @keyframes wobbleOut{
    0%{
      opacity: 1;
    }
    50%{
      opacity: .8;
    }
    70%{
      transform: translateX(60px);
      opacity: .6;
    }
    80%{
      transform: translateX(0);
    }
    100%{
      opacity: 0;
      transform: translateX(-60px);
    }

  }

</style>