<template>
  <v-app>
    <v-app-bar elevation="5" class="app-bar">
      <v-text-field
        prepend-inner-icon="mdi-magnify"
        placeholder="Search"
        variant="outlined"
        hide-details
        density="compact"
        class="search-bar"
      ></v-text-field>

      <v-spacer></v-spacer>

      <v-btn icon @click="toggleTheme">
        <v-icon>{{ isDark ? 'mdi-weather-sunny' : 'mdi-weather-night' }}</v-icon>
      </v-btn>

      <v-avatar size="36" class="ml-3">
        <img
          src="https://randomuser.me/api/portraits/men/85.jpg"
          alt="Avatar"
        />
      </v-avatar>
    </v-app-bar>
  </v-app>
</template>

<script>
export default {
  name: "CustomAppBar",
  data() {
    return {
      isDark: false,
    };
  },
  methods: {
    toggleTheme() {
      this.isDark = !this.isDark;
      this.$vuetify.theme.global.name = this.isDark ? "dark" : "light";
    },
  },
};
</script>


<style src="./AppBar.css"></style>
