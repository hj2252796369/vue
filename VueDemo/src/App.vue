<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <TodoHeader :addTodo="addTodo"/>
        <TodoList :todos="todos" :deleteTodo="deleteTodo"/>
        <TodoFooter  :todos="todos" :deleteAllTodo="deleteAllTodo" :selectAll="selectAll"/>


      </div>
    </div>
  </div>
</template>

<script>
  import TodoHeader from "./components/TodoHeader"
  import TodoList from "./components/TodoList"
  import TodoFooter from "./components/TodoFooter"

  export default {
    name: "App",
    data(){
      return{
        todos:[
          {"content": "学习", "status": false},
          {"content": "打游戏", "status": true},
          {"content": "其他", "status": false}]
      }
    },
    components: {
      TodoHeader, TodoList, TodoFooter
    },
    methods:{
      addTodo(todo){
        this.todos.unshift(todo);
      },
      deleteTodo(index){
        this.todos.splice(index, 1);
      },
      deleteAllTodo(){
        this.todos = this.todos.filter(todo => !todo.status )
      },
      selectAll(value){
        this.todos.forEach(todo=>{
          todo.status = value
        })
      }
    }
  }
</script>

<style scoped>
  /*base*/
  body {
    background: #fff;
  }

  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }

  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }

  .btn:focus {
    outline: none;
  }


  /*app*/
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }

  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }

</style>
