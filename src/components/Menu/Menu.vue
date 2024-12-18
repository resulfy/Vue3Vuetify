<script>
import { computed } from 'vue';

export default {
  data() {
    return {
      drawer: true,
      rail: true,
      showHoverBtn: false,
    };
  },
  computed: {
    chevronColor(){
      return this.$vuetify.theme.global.name === "dark" ? "white" : "black";
    },
    reverseColor(){
      return this.$vuetify.theme.global.name === "white" ? "dark" : "black";
    },
  }
};
</script>

<template>
  <v-card>
      <v-navigation-drawer v-model="drawer" elevation="5" :rail="rail" permanent @click="rail = false"
        @mouseenter="showHoverBtn = true" @mouseleave="showHoverBtn = false">
        <v-list-item prepend-icon="mdi-cloud" title="Narbulut" nav class="narbulut-title">
          <template v-slot:title>
            <span class="narbulut-title">Narbulut</span>
          </template>
          <template v-slot:prepend>
            <v-icon :class="{ 'mdi-cloud': true, 'icon-big': drawer && !rail }"></v-icon>
          </template>
          <template v-slot:append>
            <v-btn :color="chevronColor" class="left-icon" icon="mdi-chevron-left" variant="text" @click.stop="rail = !rail"></v-btn>
          </template>

        </v-list-item>

        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item prepend-icon="mdi-home-city" title="Home" value="home" @click="$router.push('/')"></v-list-item>
          <v-list-item prepend-icon="mdi-account" title="My Account" value="account"></v-list-item>
          <v-list-item prepend-icon="mdi-account-group-outline" title="Users" value="users" @click="$router.push('/users')"></v-list-item>
        </v-list>
      </v-navigation-drawer>
  </v-card>
</template>


<style src="./Menu.css"></style>

