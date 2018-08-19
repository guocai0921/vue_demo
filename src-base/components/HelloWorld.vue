<template>
    <div>
      <p class="msg">{{msg}}</p>
    </div>
</template>

<script>
// 配置对象与Vue一致
export default {
// 必须写函数
  data () {
    return {
      msg: 'Hello Components'
    }
  }
}
</script>

<style>
  .msg {
    color: red;
    font-size: 30px;
    font-style: italic;
    font-weight: bold;
  }
</style>
