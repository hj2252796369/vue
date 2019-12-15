<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <!--<TodoHeader @addTodo="addTodo"/>  &lt;!&ndash;给TodoHeader绑定addTodo事件&ndash;&gt;-->
        <TodoHeader ref="header"/>  <!--给TodoHeader绑定addTodo事件-->
        <TodoList :todos="todos" />
        <TodoFooter  :todos="todos" :deleteAllTodo="deleteAllTodo" :selectAll="selectAll"/>
      <todo-footer>
        <input type="checkbox" v-model="checkAll" slot="allCheck"/>
        <button class="btn btn-danger" v-show="todos.length" @click="deleteAllTodos"  slot="button">清除已完成任务</button>
        <span slot="count"><span>已完成{{completeSize}}</span> / 全部{{todos.length}}</span>
      </todo-footer>

      </div>
    </div>
  </div>
</template>

<script>
  import TodoHeader from "./components/TodoHeader"
  import TodoList from "./components/TodoList"
  import TodoFooter from "./components/TodoFooter"
  import Pubsub from "pubsub-js"
  import  sourceUtil from "./utils/sourceUtils"

  export default {
    name: "App",
    data(){
      return {
        //从localStorage 读取todos   保证刷新页面值不会发生改变
        todos: sourceUtil.readTodos()
      }
    },
    computed:{
      completeSize(){
        return this.todos.reduce((preTotal, todo) => preTotal + (todo.status?1:0), 0);
      },
      checkAll:{
        get(){
          return this.completeSize === this.todos.length && this.completeSize > 0
        },
        set(value){
          this.selectAll(value)
        }
      }
    },
    components: {
      TodoHeader, TodoList, TodoFooter
    },
    mounted(){  // 处理异步代码块  （html加载完成后执行。执行顺序：子组件-父组件）
      // this.$on('addTodo', this.addTodo);
      this.$refs.header.$on('addTodo', this.addTodo);
      //订阅信息
      Pubsub.subscribe("deleteTodo",(msg, index)=>{
        this.deleteTodo(index);
      })
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
      },
      deleteAllTodos(){
        if(window.confirm("确认删除么？")){
          this.deleteAllTodo();
        }
      }
    },
    watch:{//监视
      todos:{
        deep:true,//深度监视
        // handler: function (value) {
        //   //将todos最新的值， 保存到localStorage中
        //   window.localStorage.setItem("todos_key", JSON.stringify(value))
        // }
        handler: sourceUtil.saveTodos
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
