<template>
    <ul>
      <li v-for="(news,index) in newsArr" :key="index">{{news}}</li>
    </ul>
</template>

<script>
  export default {
    name: 'News',
    data () {
      return{
        newsArr:['美女','野兽','战狼']
      }
    }
  }
</script>

<style scoped>

</style>
