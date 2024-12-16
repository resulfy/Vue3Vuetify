<template>
  <v-app>
    <v-main>
      <div class="layout-container">
      <Menu />
      <div class="main-content">
        <div class="app-bar">
          <AppBar />
        </div>
        <div class="content">
        </div>
      </div>
    </div>
    </v-main>
  </v-app>
</template>

<script>
import Menu from "./components/Menu/Menu.vue";
import AppBar from "./components/AppBar/AppBar.vue";

export default {
  name: "App",
  components: {
    Menu,
    AppBar,
  },
};
</script>

<style src="./App.css"></style>
