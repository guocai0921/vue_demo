<template>
  <div>
    <ul>
      <li v-for="(message,index) in messagesArr" :key="message.id">
        <router-link :to="`/home/message/detail/${message.id}`">{{message.title}}</router-link>
        <button @click="pushShow(message.id)">push查看</button>
        <button @click="replaceShow(message.id)">replace查看</button>
      </li>
    </ul>
    <hr style="height:2px;border:none;border-top:5px dotted #185598;"/>
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    name: 'Message',
    data () {
      return {
        messagesArr:[]
      }
    },

    methods: {
      pushShow(id) {
        this.$router.push(`/home/message/detail/${id}`)
      },
      replaceShow() {
        this.$router.push(`/home/message/detail/${id}`)
      }
    },

    mounted (){
      const messagesArr = [
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
      this.messagesArr = messagesArr
    }
  }
</script>

<style scoped>

</style>
