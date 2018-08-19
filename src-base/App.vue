<template>
  <div id="app">
    <img src="./assets/logo.png">
    <!--3.使用组件标签-->
    <HelloWorld/>
  </div>
</template>

<script>
// 1.引入标签
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    // 2.映射组件标签
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: '微软雅黑';
  width: 200px;
  height: 200px;

}
</style>
