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
      return {
        //从localStorage 读取todos   保证刷新页面值不会发生改变
        todos: JSON.parse(window.localStorage.getItem("todos_key") || '[]')
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
    },
    watch:{//监视
      todos:{
        deep:true,//深度监视
        handler: function (value) {
          //将todos最新的值， 保存到localStorage中
          window.localStorage.setItem("todos_key", JSON.stringify(value))
        }
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
