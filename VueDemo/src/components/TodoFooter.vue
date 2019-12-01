<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="checkAll"/>
    </label>
    <span>
          <span>已完成{{completeSize}}</span> / 全部{{todos.length}}
        </span>
    <button class="btn btn-danger" v-show="todos.length" @click="deleteAllTodos">清除已完成任务</button>
  </div>
</template>

<script>
    export default {
      name: "TodoFooter",
      props:{
        todos: Array,
        deleteAllTodo: Function,
        selectAll: Function
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
      methods:{
        deleteAllTodos(){
          if(window.confirm("确认删除么？")){
            this.deleteAllTodo();
          }
        }
      }
    }
</script>

<style scoped>
  /*footer*/
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }

</style>
