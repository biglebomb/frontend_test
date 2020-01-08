<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
      hide-on-scroll
    >
      <div class="d-flex align-center">
        <v-img
          alt="Sekolahmu Logo"
          class="shrink mr-2 image-white"
          contain
          src="@/assets/sekolahmu.png"
          transition="scale-transition"
        />
      </div>
    </v-app-bar>

    <v-content>
      <Landing/>
    </v-content>
  </v-app>
</template>

<script>
import Landing from "./components/Landing";

export default {
  name: 'App',

  components: {
    Landing
  },

  data: () => ({
    //
  }),
};
</script>

<style scoped>
  .image-white {
    filter: brightness(0) invert(1);
    -webkit-filter: brightness(0) invert(1);
  }
</style>
