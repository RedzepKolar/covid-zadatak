<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center"></div>
     
      <v-toolbar-title>Legit Covid App</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-main>
      <CovidCountries />
    </v-main>
  </v-app>
</template>

<script>

import CovidCountries from "./screen/CovidCountries.vue";

export default {
  name: "App",

  components: {
    CovidCountries,
  },

  data: () => ({

  }),
};
</script>
