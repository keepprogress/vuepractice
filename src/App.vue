<template>
  <div class="app">
    <form-parent-component />
  </div>
</template>

<script>
import FormParentComponent from './components/FormParentComponent.vue'

export default {
  name: 'App',
  components: {
    FormParentComponent
  },
  data () {
    return {
    }
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
