<template>
  <div>
    <v-navigation-drawer v-model="sidebar" app>
      <v-list>
        <v-list-item-group>
          <v-list-item
            v-for="item in menuItems"
            :key="item.title"
            :to="item.path">
            <v-list-item-content class="nav-button">{{ item.title }}</v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="primary"
      light
      class="nav-bar"
      extended
      flat
    >
      <div ref="animLogo" class="anim-logo">
        <router-link :to="{ name: 'Home'}">
          <v-img src="@/../public/img/cant_image.png" />
        </router-link>
      </div>
      <div class="d-sm-none">
        <v-app-bar-nav-icon  @click="sidebar = !sidebar">
        </v-app-bar-nav-icon>
      </div>
      <div class="d-none d-md-block left-padding"></div>
      <div class="d-flex align-center">
        <div ref="mainLogo" class="regular-logo">
          <router-link :to="{ name: 'Home'}">
            <v-img
              alt="Cant Logo"
              class="shrink mr-2"
              contain
              src="@/../public/img/cant_image.png"
              v-resize="onResize"
              :max-width="windowSize.x - logoMaxSizeBuffer"
              width="300"
              height="300"
            />
          </router-link>
        </div>
      </div>

      <v-spacer></v-spacer>

      <v-btn
        :to="{ name: 'Work'}"
        text
        class="d-none d-sm-block"
      >
        <span class="nav-button">Work</span>
      </v-btn>
      <v-btn
        :to="{ name: 'About'}"
        text
        class="d-none d-sm-block"
      >
        <span class="nav-button">About</span>
      </v-btn>
      <div class="d-none d-md-block right-padding"></div>
    </v-app-bar>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
import { Watch } from 'vue-property-decorator';
import { TimelineMax, gsap } from 'gsap';
import { CSSPlugin } from 'gsap/CSSPlugin';

gsap.registerPlugin(CSSPlugin);

@Component
export default class NavBar extends Vue {
  $refs!: {
    mainLogo: HTMLDivElement;
    animLogo: HTMLDivElement;
  }

  @Watch('$route.name')
  onPropertyChanged() {
    this.setupAnimation();
  }

  sidebar = false;

  menuItems = [
    { title: 'Work', path: '/work' },
    { title: 'About', path: '/about' },
    { title: 'Contact', path: '/contact' },
  ]

  windowSize = { x: 0, y: 0 }

  private logoMaxSizeBuffer = 80;

  private timeline: TimelineMax | undefined;

  private requestId: number | null = null;

  private triggerOffset = 0;

  private duration = 300;

  private sceneStart = 0;

  private animationComplete = false;

  // lifecycle hook
  mounted() {
    this.onResize();
    this.setupAnimation();
  }

  private onResize() {
    this.windowSize = { x: window.innerWidth, y: window.innerHeight };
  }

  private setupAnimation(): void {
    if (this.animateLogo()) {
      this.timeline = new TimelineMax({
        paused: true,
      });
      const start = NavBar.getStart();
      const target = this.getTarget();
      this.$refs.animLogo.style.width = `${start.width}px`;
      this.$refs.animLogo.style.height = `${start.height}px`;
      this.$refs.animLogo.style.top = `${start.y}px`;
      this.$refs.animLogo.style.left = `${start.x}px`;
      this.$refs.animLogo.style.display = 'block';
      this.$refs.mainLogo.style.display = 'none';
      this.timeline
        .to('.anim-logo', this.duration, {
          width: target.width, height: target.height, x: target.x - start.x, y: target.y - start.y,
        }, this.sceneStart)
        .set('.regular-logo', { display: 'flex' })
        .set('.anim-logo', { display: 'none' });
      // Only update on animation frames
      window.addEventListener('scroll', this.scrollUpdate);
      this.updateAnimation();
    } else {
      // double check that the main logo is not hidden
      if (this.timeline !== undefined) {
        // seek to the start as killing in the middle of an animation seems
        // to cause bugs when recreating a new timeline
        // specifically in our case, the translation of the new timeline will not update
        this.timeline.seek(0).kill();
        this.timeline = undefined;
        window.removeEventListener('scroll', this.scrollUpdate);
      }
      this.$refs.mainLogo.style.display = 'flex';
      this.$refs.animLogo.style.display = 'none';
    }
  }

  private scrollUpdate() {
    if (!this.requestId) {
      this.requestId = requestAnimationFrame(this.updateAnimation);
    }
  }

  private static getStart(): {x: number; y: number; width: number; height: number} {
    const width = window.innerWidth * 0.3 + 60; // +60 for small screens
    const height = width * 0.23;
    const x = window.innerWidth * 0.144;
    const y = (window.innerWidth * 0.3) / 2.2 + 100; // +100 for small screens
    return {
      x, y, width, height,
    };
  }

  private getTarget(): {x: number; y: number; width: number; height: number} {
    const logo = this.$refs.mainLogo;
    const rect = logo.getBoundingClientRect();
    const result = {
      x: rect.left, y: rect.top, width: rect.width, height: rect.height,
    };
    if (rect.width > this.windowSize.x - this.logoMaxSizeBuffer) {
      result.width = this.windowSize.x - this.logoMaxSizeBuffer;
    }
    return result;
  }

  private animateLogo() {
    return this.$route.name === 'Home';
  }

  private updateAnimation() {
    if (this.timeline !== undefined) {
      this.timeline.time(window.pageYOffset + this.triggerOffset);
      this.requestId = null;
    }
  }
}
</script>
<style lang="scss" scoped>
.nav-bar {
  padding-top: 16px;
}
.left-padding {
  padding-left: 140px;
}
.right-padding {
  padding-right: 140px !important;
}
.anim-logo {
  position: absolute;
}
</style>
