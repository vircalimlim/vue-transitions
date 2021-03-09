<template>
  <transition name="title" appear>
  <h1>Transitions</h1>
  </transition>
  <form @submit.prevent="addTodo">
    
    <transition 
    name="alert"
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter"
    @before-leave="beforeLeave"
    @leave="leave"
    @after-leave="afterLeave"
    >
    <div v-if="error" class="error alert">{{error}}</div>
    </transition>
    
    <input type="text" v-model="todo">
    <br>
    <input type="submit" value="Add To Do">
    
    <transition-group tag="ul" name="alert" appear>
    <li v-for="todoitem in todolist" :key="todoitem" @click.self="removeItem">{{todoitem}}</li>
    </transition-group>
    
  </form>
</template>

<script>
  export default {
    data(){
      return{
        todo: '',
        todolist: ['basketball', 'programming'],
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
      },
      
        beforeEnter(e){
          alert("before")
        },
        
        enter(e){
          alert("enter")
        },
        
        afterEnter(e){
          alert(e.style.backgroundColor = "skyblue")
        },
        
        beforeLeave(e){
          alert("before")
        },
        
        leave(e){
          alert("leave")
        },
        
        afterLeave(e){
          alert(e.style.backgroundColor = "crimson")
        },
    }
    
  }
</script>

<style scoped>
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
  
  .alert-enter-from, .alert-leave-to{
    opacity: 0;
    transform: translateX(-90px);
  }
  .alert-enter-to, .alert-leave-from{
    opacity: 1;
    transform: translateX(0);
    
  }
  .alert-enter-active, .alert-leave-active{
    transition: all 2s ease;
  }
  
  
  
  .title-enter-from{
    opacity: 0;
    transform: translateY(-80px);
  }
  .title-enter-active{
    transition: all .6s ease;
  }
</style>