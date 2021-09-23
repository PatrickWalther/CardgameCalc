<template>
  <v-app>
    <Navbar />
    <v-main>
      <Calculator />
    </v-main>
  </v-app>
</template>

<script>
import Calculator from './components/Calculator';
import Navbar from "./components/Navbar"

export default {
  name: "App",
  components: {
    Navbar,
    Calculator,
    
  },
  data: () => ({
  }),
  mounted() {
    const theme = localStorage.getItem("dark_theme");
    if (theme) {
        if (theme == "true") {
            this.$vuetify.theme.dark = true;
        } else {
            this.$vuetify.theme.dark = false;
        }
    }
  },
};
</script>
