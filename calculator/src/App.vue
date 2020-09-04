<template>
  <v-app>
    <v-navigation-drawer
      v-model="primaryDrawer.model"
      :clipped="false"
      :floating="false"
      :mini-variant="false"
      app
      :expand-on-hover="true"
      overflow
    >
      <v-list>
        <v-list-item
          v-for="item in primaryDrawer.items"
          :key="item.title"
          link
          :to="item.link"
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

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
      <v-spacer />
      <span class="px-4">
        <v-icon>{{ icons.mdiGithub }}</v-icon> View on GitHub
      </span>
    </v-footer>
  </v-app>
</template>

<script>
import {
  mdiViewDashboard,
  mdiCalculator,
  mdiHelpBox,
  mdiGithub,
} from "@mdi/js";

export default {
  name: "App",

  data: () => ({
    primaryDrawer: {
      model: true,
      items: [
        { title: "Home", icon: mdiViewDashboard, link: "/" },
        { title: "Help", icon: mdiHelpBox, link: "help" },
        { title: "Calculator", icon: mdiCalculator, link: "calculator" },
      ],
    },
    icons: {
      mdiGithub: mdiGithub,
    },
  }),
};
</script>
