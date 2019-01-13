<template>
  <div id="app">
    <!--<HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <Reminder/>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Reminder from "./components/Reminder.vue";

export default {
  name: "app",
  components: {
    HelloWorld,
    Reminder
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
#app img {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
</style>
