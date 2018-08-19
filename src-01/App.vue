<template>
    <div>
      <header class="site-header jumbotron">
        <div class="container">
          <div class="row">
            <div class="col-xs-12">
              <h1>请发表对Vue的评论</h1>
            </div>
          </div>
        </div>
      </header>
      <div class="container">
        <Add :addComment="addComment"/>
        <list :comments="comments" :deleteComment="deleteComment"/>
      </div>
    </div>
</template>

<script>
  import Add from './components/Add.vue'
  import List from './components/List.vue'

  export default {
    data () {
      return {
        comments: [
          {
            name: 'BOB',
            content: 'Vue is so easy'
          },
          {
            name: 'ROSE',
            content: 'Vue is so difficult'
          }

        ]
      }
    },
    methods: {
      // 添加评论
      addComment (comment){
        this.comments.unshift(comment)
      },
      // 删除指定下标的评论
      deleteComment (index) {
        this.comments.splice(index,1)
      }
    },
    components:{
      Add,
      List
    }
  }
</script>

<style>

</style>
