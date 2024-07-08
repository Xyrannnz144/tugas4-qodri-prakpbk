<template>
  <div id="app">
    <EmployeeManagement />
  </div>
</template>

<script>
import EmployeeManagement from './views/EmployeeManagement.vue';

export default {
  components: {
    EmployeeManagement
  }
};
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
