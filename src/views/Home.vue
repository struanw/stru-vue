<template>
  <div>
    <v-img v-resize="onResize" position="bottom" :max-height="imageHeight"
      src="@/../public/img/cant_image.png">
    </v-img>
    <div class="spacer" />
    <v-container>
      <v-row>
        <v-col cols=12>
          <hero-card
            title="Web Development"
            src="/img/cant_image.png"
            max-width="966"
            description="We work with companies of all sizes to create custom
            websites and web apps. We can take you through the development
            cycle that will result in a great web experience to reach your
            customers. We offer hosting options to match your needs. "
          />
        </v-col>
        <v-col cols=12>
          <hero-card
            title="Consulting"
            imageRight=true
            src="/img/home/pink.png"
            max-width="966"
            description="We provide a broad range of consulting services
            to get your business the most out of the cloud. We can
            provide advice on application architecture, deployment
            strategies and which cloud services can be leveraged to build
            your system faster. We can also help with implementing your
            system and deployment processes."
          />
        </v-col>
      </v-row>
    </v-container>
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
  height: 190px;
}
</style>
