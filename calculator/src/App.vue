<template>
  <v-app>
    <v-navigation-drawer
      v-model="primaryDrawer.model"
      :clipped="false"
      :floating="false"
      :mini-variant="false"
      app
      overflow
    ></v-navigation-drawer>

    <v-app-bar :clipped-left="false" app>
      <v-app-bar-nav-icon
        @click.stop="primaryDrawer.model = !primaryDrawer.model"
      ></v-app-bar-nav-icon>
      <v-toolbar-title>Anno 1800 Calculator</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>

    <v-footer :inset="false" app>
      <span class="px-4"
        >&copy; {{ new Date().getFullYear() }} Daniel Tomlinson</span
      >
    </v-footer>
  </v-app>
</template>

<script>

export default {
  name: "App",

  data: () => ({
    primaryDrawer: {
      model: true,
    },
  }),
};
</script>
