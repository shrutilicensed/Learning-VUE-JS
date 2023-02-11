<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <Introduction msg="Shruti" />
    <CustomerTable />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

// It is not necessary to give this the same name as the one we have exported
import Introduction from "./components/test.vue";

import CustomerTable from "./components/assignment.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    Introduction,
    CustomerTable,
  },
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
