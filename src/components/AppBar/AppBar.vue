<template>
  <v-app>
      <v-app-bar elevation="5" class="app-bar">
      <v-text-field
        prepend-inner-icon="mdi-magnify"
        placeholder="Search"
        variant="plain"
        hide-details
        density="compact"
        class="search-bar"
      ></v-text-field>

      <v-spacer></v-spacer>
      <div class="bar-buttons">
        <v-btn icon @click="toggleTheme">
        <v-icon>{{ isDark ? 'mdi-weather-sunny' : 'mdi-weather-night' }}</v-icon>
      </v-btn>

      <v-menu
            offset-y
            close-on-content-click
          >

            <template #activator="{ props }">
              <v-avatar size="36" v-bind="props" class="ml-3">
                <img
                  src="https://randomuser.me/api/portraits/men/85.jpg"
                  alt="Avatar"
                />
              </v-avatar>
            </template>

            <v-list>
              <v-list-item title="Settings" prepend-icon="mdi-cog" @click="settings"></v-list-item>
              <v-list-item title="Log Out" prepend-icon="mdi-logout" @click="logout"></v-list-item>
            </v-list>
          </v-menu>
      </div>
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
    logout() {
      console.log("Log Out clicked");
    },
    settings() {
      console.log("Settinga clicked");
    }
  },
};
</script>


<style src="./AppBar.css"></style>
