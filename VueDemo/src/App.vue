<template>
  <div>
    <img class="img" src="./assets/logo.png">
    <HelloWorld/>
  </div>
</template>

<script>
  import HelloWorld from "./components/HelloWorld.vue"

  export default {
    name: 'App',
    components:{
      HelloWorld
    }
  }
</script>

<style scoped>
.img{
  width: 800px;
  height: 400px;
}
</style>
