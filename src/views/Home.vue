<template>
  <div>
    <div class="spacer" />
    <v-container>
      <v-row>
        <v-col cols=12>
          <hero-card
            imageRight=true
            src="/img/home/billmurray.png"
            max-width="966"
            description="This is an adventure."

          />
        </v-col>
      </v-row>
    </v-container>
    <div class="spacerBottom" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
import HeroCard from '../components/HeroCard.vue';

@Component({
  components: {
    HeroCard,
  },
})
export default class Home extends Vue {
  windowSize = { x: 0, y: 0 }

  imageHeight = '0px';

  mounted() {
    this.onResize();
  }

  onResize() {
    this.windowSize = { x: window.innerWidth, y: window.innerHeight };
    this.imageHeight = `${this.windowSize.y * 0.9}px`;
  }
}
</script>

<style lang="scss" scoped>
.spacer {
  height: 680px;
}
.spacerBottom {
  height: 300px;
}
</style>
