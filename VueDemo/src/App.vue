<template>
  <div id="app">
    <div class="container">
      <search/>
      <UserMain/>

    </div>
  </div>
</template>

<script>

  import Pubsub from "pubsub-js"
  import search  from "./components/search"
  import  main from "./components/main"

  export default {
    name: "App",
    components:{
      search,
      UserMain: main
    }
  }
</script>

<style scoped>


</style>
