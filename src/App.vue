<template>
  <div id="app">
    <h1>备忘录</h1>
    <HelloWorld msg="计划要做什么呢？"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  }
}
</script>

<style lang="less">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  h1{
    color: #ead7d7;
  }
}
body{
  background-color: #f5f5f5;

}
</style>
