<template>

  <div class="container">
    <Search/>
    <UsersMain/>
  </div>

</template>

<script>
  import Search from './components/Search.vue'
  import Main from './components/Main.vue'
  export default {
    components:{
      Search,
      UsersMain:Main
    }
  }
</script>

<style>
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
