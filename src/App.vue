<template>
  <v-app>
    <Menu />
  </v-app>
</template>

<script>
import Menu from "./components/Menu/Menu.vue";

export default {
  name: "App",
  components: {
    Menu,
  },
};
</script>

<style src="./App.css"></style>
