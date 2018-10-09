<template>
  <div id="app">
    <SchemaBuilder></SchemaBuilder>
  </div>
</template>

<script>
import SchemaBuilder from './components/SchemaBuilder.vue'
// import Polaris from './components/Polaris.vue'

export default {
  name: 'app',
  components: {
    SchemaBuilder
    // Polaris
  }
}
</script>


<style lang="scss">


#app {
  // font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
