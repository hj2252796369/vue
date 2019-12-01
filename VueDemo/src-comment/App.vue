<template>
  <div>
    <header class="site-header jumbotron">
      <div class="container">
        <div class="row">
          <div class="col-xs-12">
            <h1>请发表对React的评论</h1>
          </div>
        </div>
      </div>
    </header>
    <div class="container">
      <Form :addComment="addComment"/>
      <List :comments="comments" :deleteComment="deleteComment"/>
    </div>
  </div>
</template>

<script>

  import Form from "./components/Form"
  import List from "./components/List"

  export default {
    name: 'App',
    data(){
      return {
        comments:[
          {
            name : "Mike",
            context: "React不错"
          },{
            name : "yyy",
            context: "React有点难"
          }
        ]
      }
    },
    methods:{
      addComment(comment){
        this.comments.unshift(comment)
      },
      deleteComment(index){
        this.comments.splice(index,1)
      }
    },
    components:{
      Form,
      List
    }
  }
</script>

<style>
  .reply {
    margin-top: 0px;
  }
</style>
