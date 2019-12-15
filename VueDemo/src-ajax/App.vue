<template>
  <div id="app">
    <div v-if="!repoUrl"> loading......</div>
    <div v-else="repoUrl"><a :href="repoUrl">最受欢迎的 ： {{repoName}}</a> </div>
  </div>
</template>

<script>

  import axios from 'axios'
  export default {
    name: "App",
    data(){
      return{
        repoUrl: '',
        repoName: ''
      }
    },
    mounted() {
      //发送ajax请求
      const url = 'https://api.github.com/search/repositories?q=v&sort=stars'
     //使用axios发送ajax请求
      axios.get(url).then(response=>{
        //成功了
        const result = response.data
        const item = result.items[0]
        this.repoUrl = item.html_url
        this.repoName = item.name
      }).catch(error=>{
        console.info(error.message)
      })
    }
  }
</script>

<style scoped>


</style>
