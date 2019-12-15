<template>
  <div class="row">
    <h1 v-if="firstStatus">请输入搜索内容.....</h1>
    <h1 v-if="secondStatus">搜索中.....</h1>
    <div class="card" v-for="(user, index) in users" :key="index">
      <a :href="user.url" target="_blank">
        <img :src="user.avatarUrl" style='width: 100px'/>
      </a>
      <p class="card-text">{{user.username}}</p>
    </div>
  </div>
</template>

<script>
import PubSub from 'pubsub-js'
import axios from 'axios'
  export default {
    name: "main",
    data(){
      return{
        firstStatus: true,
        secondStatus: false,
        users: null,
        errorMsg: ""
      }
    },
    mounted() {
      //订阅消息
      PubSub.subscribe('search',(msg, searchName) =>{
        const url = 'https://api.github.com/search/users?q=' + searchName;
        //发送请求之前更新状态
        //请求中
        this.firstStatus = false
          this.secondStatus = true
        this.users = null
        this.errorMsg = ''

        axios.get(url).then((response)=>{
          const result = response.data
          const users = result.items.map(item => ({
            url: item.url,
            avatarUrl: item.avatar_url,
            username: item.login
          }))

          this.users = users
          console.info( this.users)
          this.secondStatus = false

        }).catch((error)=>{
          this.secondStatus = false
          this.errorMsg = error.errorMsg
        })
      })
    }

  }
</script>

<style scoped>

</style>
