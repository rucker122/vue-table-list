<template>
  <h1>Aye</h1>
  <table-list></table-list>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import TableList from './components/TableList.vue'

export default {
  name: 'App',
  components: {
    TableList
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
