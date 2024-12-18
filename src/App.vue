<script>
import Menu from "./components/Menu/Menu.vue";
import AppBar from "./components/AppBar/AppBar.vue";
import UserTable from "./components/UserTable/UserTable.vue";

export default {
  name: "App",
  components: {
    Menu,
    AppBar,
  },
};
</script>

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
          <router-view></router-view>
        </div>
      </div>
    </div>
    </v-main>
  </v-app>
</template>

<style src="./App.css"></style>
