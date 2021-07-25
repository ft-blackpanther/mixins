<template>
  <div id="app">
    <Test1 />
    <br />
    <Test2 />
    <br />
    <Test3 />
  </div>
</template>

<script>
import Test1 from './components/Test1.vue'
import Test2 from './components/Test2.vue'
import Test3 from './components/Test3.vue'

export default {
  name: 'App',
  components: {
    Test1,
    Test2,
    Test3,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
