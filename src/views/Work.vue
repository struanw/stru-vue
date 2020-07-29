<template>
  <v-container class="parent">
    <h1 class="child">Past Work</h1>
    <v-container class="work-cards">
      <hero-card
        title=""
        src=""
        href=""
        max-width="966"
        description="Stuff."
      />
      <hero-card
        title=""
        src=""
        max-width="966"
        description="."
      />
   <hero-card
        title=""
        src=""
        max-width="966"
        description="A."
      />
      <hero-card
        title=""
        src=""
        max-width="966"
        href=""
        description="Ma."
      />
    </v-container>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HeroCard from '../components/HeroCard.vue';

@Component({
  components: {
    HeroCard,
  },
})
export default class Work extends Vue {
}
</script>

<style lang="scss" scoped>
.parent {
  text-align: center;
}
.work-cards {
  display: inline-block;
}
.child {
  margin: auto;
}
</style>
