<template>
    <div class="msg">{{msg}}</div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data(){
      return{
        msg:"Hello World"
      }
    }
  }
</script>

<style scoped>
  .msg{
    font-size: 30px;
  }
</style>
