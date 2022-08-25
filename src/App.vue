<template>
  <div id="app">
    <Recursive />
  </div>
</template>


<script>
import Recursive from "./components/Recursive/Recusive.vue";
export default {
  name: "app",
  components: {
    Recursive
  },
  methods: {
    handleEdit(item) {
      switch (item.type) {
        case "edit":
          this.listUser[item.index].name = item.name;
          break;
        case "delete":
          this.listUser.splice(item.index, 1);
          break;
        case "add":
          this.listUser.push(item.user);
          break;
        default:
          break;
      }
    },
  },
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

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
