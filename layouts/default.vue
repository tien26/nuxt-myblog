<template>
  <v-app dark>
    <v-app-bar fixed app center>
      <v-toolbar-title class="text-h4">{{ title }}</v-toolbar-title>
      <v-spacer></v-spacer>
      <div v-for="(item, i) in items" :key="i">
        <v-btn :to="item.to" width="100" color="grey" class="mx-3">
          {{ item.title }}
        </v-btn>
      </div>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-apps",
          title: "Home",
          to: "/",
        },
        {
          icon: "mdi-chart-bubble",
          title: "Admin",
          to: "/admin",
        },
      ],
      miniVariant: false,
      right: false,
      rightDrawer: false,
      title: "Vuetify.js",
    };
  },
};
</script>
