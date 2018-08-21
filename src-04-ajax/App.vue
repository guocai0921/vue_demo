<template>
  <div class="todo-container">
    <div v-if="!repoUrl">loading</div>
    <div v-else>most star repo is <a :href="repoUrl">{{repoName}}</a></div>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    data () {
      return {
        repoUrl: '',
        repoName: ''
      }
    },
    mounted (){
      // // 发送ajax请求
      const url = `https://api.github.com/tsearch/repositories?q=vu&sort=stars`
      // this.$http.get(url).then(
      //   (response) => {
      //     const result = response.data
      //     const mostRepo = result.items[0]
      //     this.repoUrl = mostRepo.html_url
      //     this.repoName = mostRepo.name
      //   },
      //   (response) => {
      //     alert('请求失败!');
      //   }
      // )
      axios.get(url).then(
        (response) => {
          const result = response.data
          const mostRepo = result.items[0]
          this.repoUrl = mostRepo.html_url
          this.repoName = mostRepo.name
        }
      ).catch((error)=>{
        alert('失败啦！请重新来过!');
      })
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
