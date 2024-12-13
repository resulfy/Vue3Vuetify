<template>
  <v-card>
    <v-layout>
      <v-navigation-drawer
        v-model="drawer"
        elevation="5"
        :rail="rail"
        permanent
        @click="rail = false"
        @mouseenter="showHoverBtn = true"
        @mouseleave="showHoverBtn = false"
      >
        <v-list-item
          prepend-avatar="https://randomuser.me/api/portraits/men/85.jpg"
          title="John Leider"
          nav
        >
          <template v-slot:append>
            <v-btn
              icon="mdi-chevron-left"
              variant="text"
              @click.stop="rail = !rail"
            ></v-btn>
          </template>

        </v-list-item>

        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item prepend-icon="mdi-home-city" title="Home" value="home"></v-list-item>
          <v-list-item prepend-icon="mdi-account" title="My Account" value="account"></v-list-item>
          <v-list-item prepend-icon="mdi-account-group-outline" title="Users" value="users"></v-list-item>
        </v-list>
        <v-list-item
        class="hover-btn"
        >
          <v-btn
            icon="mdi-chevron-right"
            variant="text"
            v-if="showHoverBtn"
        ></v-btn>
        </v-list-item>
      </v-navigation-drawer>
      <v-main style="height: 250px"></v-main>
    </v-layout>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      drawer: true,
      rail: true,
      showHoverBtn: false,
    };
  },
};
</script>


<style src="./Menu.css"></style>

