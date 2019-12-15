<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="content" @keyup.enter="add()"/>
  </div>
</template>

<script>
    export default {
        name: "TodoHeader",
      props:{
        // addTodo: Function
      },
      data(){
          return{
            content:""
          }
      },
      methods:{
        add(){
          //1、 验证数据
          const content = this.content;
          //2、 封装数据
          if(!content){
            alert("输入值不能为空");
            return
          }
          const todo = {
            "content":content,
            "status": false
          }
          //3、 添加
          // this.addTodo(todo);
          this.$emit('addTodo', todo);
          //4、 清空
          this.content = "";
          }
      }
    }
</script>

<style scoped>
  /*header*/
  .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
  }

  .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
  }

</style>
