<template>
  <div id="app">
    <power/>
  </div>
</template>

<script>
  import power from "./components/power.vue"

export default {
  name: 'App',
  components: {
    power
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
background-color: rgb(228, 156, 102);
}
</style>
