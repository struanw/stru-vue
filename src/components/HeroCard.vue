<template>
    <div>
              <div>
                <v-container>
                  <v-row>
                    <v-col :xs="12"
                    :sm="8 + noneImageExpand"
                    :md="8 + noneImageExpand"
                    :lg="8 +noneImageExpand"
                    :xl="8 + noneImageExpand">
                      <div>
                        <v-card-title
                          class="headline"
                          v-bind:class="{
                            'flex-row': !imageRight,
                            'flex-row-reverse': imageRight && !$vuetify.breakpoint.xsOnly
                            }"
                        ><h2>{{title}}</h2></v-card-title>
                        <v-card-subtitle
                          v-bind:class="{
                            'left-align': !imageRight,
                            'right-align': imageRight && !$vuetify.breakpoint.xsOnly
                            }"
                        >
                          <div
                            v-bind:class="{'div-on-right': imageRight &&
                              !$vuetify.breakpoint.xsOnly}"
                          />
                          <p>{{description}}</p>
                        </v-card-subtitle>
                      </div>
                    </v-col>

                    <v-col v-if="displayImage && (imageRight && ! $vuetify.breakpoint.xsOnly)"
                      :xs="12" :sm="4" :md="4" :lg="4" :xl="4">
                      <v-avatar
                        size="320"
                      >
                        <v-img :src="src"></v-img>
                      </v-avatar>
                    </v-col>
                  </v-row>
                </v-container>
              </div>
            </a>
          </v-card>
    </div>

</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
import { Prop } from 'vue-property-decorator';

@Component
export default class HeroCard extends Vue {
    @Prop({ required: false })
    public src: string | undefined;

    @Prop({ required: true })
    public title!: string;

    @Prop({ required: true })
    public description!: string;

    @Prop({ default: 0 })
    public maxWidth!: number;

    @Prop({ default: false })
    public imageRight!: boolean;

    @Prop({ required: false })
    public href: string | undefined;

    public get width(): unknown {
      if (this.maxWidth !== 0) {
        return { 'max-width': this.maxWidth };
      }
      return {};
    }

    public get displayImage(): boolean {
      if (this.src === undefined || this.src === null || this.src === '') {
        return false;
      }
      return true;
    }

    public get createLink(): boolean {
      if (this.href === undefined || this.href === null || this.href === '') {
        return false;
      }
      return true;
    }

    public get noneImageExpand(): number {
      if (!this.displayImage) {
        return 4;
      }
      return 0;
    }
}
</script>

<style lang="scss" scoped>
h2 {
  word-break: break-word;
}

.div-on-right {
  margin-left: auto;
}
.right-align {
  text-align: justify;
}
.left-align {
  text-align: justify;
}
</style>
