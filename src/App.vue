<template>
  <div id="app">
    <img width="25%" src="./assets/logo.png">
    <DragTree  :list.sync="menus"  ref="tree"/>
  </div>
</template>

<script>
import DragTree from "./components/DragTree.vue";

export default {
  name: "App",
  data() {
    return {
      menus: [{"id":213,"name":"DDD","subs":[{"id":214,"name":"11111","subs":[],"index":0}],"index":0},{"id":174,"name":"aaa","subs":[],"index":1},{"id":173,"name":"bbb","subs":[],"index":2},{"id":216,"name":"EEE","subs":[{"id":217,"name":"222","subs":[],"index":0}],"index":3},{"id":425,"name":"222222","subs":[],"index":4}]
    }
  },
  components: {
    DragTree
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
