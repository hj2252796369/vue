<template>
  <div class="col-md-4">
    <form class="form-horizontal">
      <div class="form-group">
        <label>用户名</label>
        <input type="text" class="form-control" placeholder="用户名" v-model="name">
      </div>
      <div class="form-group">
        <label>评论内容</label>
        <textarea class="form-control" rows="6" placeholder="评论内容" v-model="context"></textarea>
      </div>
      <div class="form-group">
        <div class="col-sm-offset-2 col-sm-10">
          <button type="button" class="btn btn-default pull-right" @click="add()">提交</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
  export default {
    name: "Form",
    props:{
      addComment:{    //指定属性名/属性质类型/是否有必要性
        type: Function,
        request: true
      }
    },
    data() {
      return {
        name: "",
        context: ""
      }
    },
    methods: {
      add(){
        //1、获取输入值
        const name = this.name;
        const context = this.context;
        if(!name || !context){
          alert("name 或者 评论不能为空");
            return;
        }
        //2、封装成对象
        const comment = {
          name,
          context
        };
        //3、保存
        this.addComment(comment);
        //4、清空表单
        this.name = "";
        this.context = "";
      }
    }
  }
</script>

<style scoped>

</style>
