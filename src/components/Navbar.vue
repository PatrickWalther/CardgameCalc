<template>
  <v-container>
    <v-app-bar>
      <!-- TODO: Add custom logo -->

      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn icon v-on:click="toggle_dark_mode">
        <v-icon>mdi-theme-light-dark</v-icon>
      </v-btn>

      <v-btn
        href="https://github.com/PatrickWalther/CardgameCalc"
        target="_blank"
      >
        <span class="mr-2">View code</span>
        <v-icon>mdi-github</v-icon>
      </v-btn>
    </v-app-bar>
  </v-container>
</template>

<script>
export default {
  name: "Navbar",
  methods: {
    toggle_dark_mode: function () {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
      localStorage.setItem("dark_theme", this.$vuetify.theme.dark.toString());
    },
  },
};
</script>