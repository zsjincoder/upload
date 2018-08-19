<template>
  <div id="app">
    <HelloWorld/>
  </div>
</template>
<script>
import HelloWorld from './components/HelloWorld'
export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  margin: 200px auto;
  padding: 0;
}
</style>
