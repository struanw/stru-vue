<template>
  <v-container class="parent">
    <h1 class="child">Past Work</h1>
    <v-container class="work-cards">
       <router-link :to="{ name: 'Gmwater'}">
      <hero-card
        title="GM Water Recycling"
        src="/img/work/gmwater.png"
        href="https://gmwater-recycling-limited.co.nz/?ref=mcalpinefree.co.nz"
        max-width="966"
        description="GM Water Recycling wanted a website where potential customers can
        get information about their product and submit enquires. We provided them with
        a website that we designed and host. We also created 3D renders from their CAD
        files for some eye catching content to display on their landing page."
      />
       </router-link>
        <router-link :to="{ name: 'Moxion'}">
      <hero-card
        title="Moxion"
        src="/img/work/domenico-loia-hGV2TfOh0ns-unsplash@2x.png"
        max-width="966"
        description="Moxion wanted to secure their AWS account structure
        and deploy their services to mainland China. We provided a solution
        using CodePipeline and CloudFormation that automated the creation
        and configration of their AWS accounts. We also automated their
        deployment to Alibaba cloud using CodePipeline and Terraform."
      />
         </router-link>
       <router-link :to="{ name: 'Alchemy'}">
   <hero-card
        title="Alchemy Agencies"
        src="/img/work/ilya-pavlov-OqtafYT5kTw-unsplash@2x.png"
        max-width="966"
        description="Alchemy Agencies wanted to provide their customers with
        access to specialty order and product information from their custom ERP
        and CRM systems in a secure and reliable way. We built an integration
        which allowed Alchemy Agencies to to give their customers a login to
        their public facing website in which the customer could access the
        relavent information based on which products they had purchased from
        Alchemy Agencies."
      />
         </router-link>
       <router-link :to="{ name: 'Maungaturoto'}">
      <hero-card
        title="Maungaturoto Storage"
        src="/img/work/maungatoroto-storage.jpg"
        max-width="966"
        href="https://maungaturotostorage.co.nz/?ref=mcalpinefree.co.nz"
        description="Maungatoroto Storage wanted an online presence and to display their
        various storage options to customers. We designed and host a single page website
        for them that provides a gallery for their storage options and pricing."
      />
         </router-link>
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
