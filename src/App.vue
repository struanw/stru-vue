<template>
  <v-app>
    <nav-bar/>
    <v-content>
      <router-view/>
    </v-content>
    <v-footer color="primary" absolute padless flat app>
      <v-col
        class="text-center footer"
        cols="12"
      >
       {{ new Date().getFullYear() }}
      </v-col>
    </v-footer>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
import NavBar from './components/NavBar.vue';

export default Vue.extend({
  name: 'App',
  components: {
    NavBar,
  },
  data: () => ({
    //
  }),
});
</script>

<style lang="sass">
@import "@/global-style.scss"
@import "https://use.typekit.net/fmd3bft.css"
</style>
