<template>
  <div>
    <p>ID:{{$route.params.id}}</p>
    <ul>
      <li >{{messageDetail.id}}</li>
      <li >{{messageDetail.title}}</li>
      <li >{{messageDetail.content}}</li>
    </ul>
  </div>
</template>

<script>

  export default {
    name: 'MessageDetails',
    data () {
      return {
        messageDetail: {},
        allMessagesArr:{}
      }
    },
    mounted () {

      const allMessagesArr = [
        {
          id: 1,
          title: 'message001',
          content: 'angular'
        },{
          id: 2,
          title: 'message002',
          content: 'react'
        },{
          id: 3,
          title: 'message003',
          content: 'vue'
        }
      ]
      this.allMessagesArr = allMessagesArr
      const id = this.$route.params.id*1

      this.messageDetail = allMessagesArr.find(detail => detail.id==id)
    },
    watch :{
      $route: function (value) {
        const id = value.params.id*1
        this.messageDetail = this.allMessagesArr.find(detail => detail.id==id)
      }
    }
  }
</script>

<style scoped>

</style>
