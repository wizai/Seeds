<template>
  <section class="page_plant">
    <div class="page_plant__img"
         :style="{ 'background-image': 'url(' + plant.image + ')' }">
      <div class="page_plant__header">
        <nuxt-link :to="{name: 'garden'}" class="page_plant__header--link">
          <i class="icon-arrow"></i>
        </nuxt-link>
      </div>
    </div>
    <div class="page_plant__actions">
      <div class="page_plant__actions--remove" @click="removePlant()">
        <span><i class="icon-delete"></i></span>
      </div>
      <div class="page_plant__actions--add" @click="showFormPlant()">
        <p><span>+</span>Add to your garden</p>
      </div>
    </div>
    <Form_plant :open="formPlant_open" :plant_id="plant.id" @hideForm="formPlant_open = false" />
    <div class="page_plant__content">
      <h1 class="page_plant__title">{{ plant.title }}</h1>
      <p class="page_plant__subtitle">{{ plant.category }}</p>
      <div class="page_plant__informations">
        <div class="page_plant__informations--row">
          <div class="page_plant__informations--date">
            <i class="icon-calendar"></i>
            <div>
              <p>Sowing</p>
              <p v-if="plant.sowed">{{ plant.sowed | moment('MMM d, YYYY') }}</p>
              <p v-else>--- - ----</p>
            </div>
          </div>
          <div class="page_plant__informations--date">
            <i class="icon-calendar"></i>
            <div>
              <p>Planting</p>
              <p v-if="plant.planted">{{ plant.planted | moment('MMM d, YYYY') }}</p>
              <p v-else>--- - ----</p>
            </div>
          </div>
        </div>
        <div class="page_plant__informations--row">
          <p class="page_plant__informations--title">Seedling</p>
          <div class="page_plant__informations--item">
            <div>
              <i class="icon-water"></i>
            </div>
            <div>
              <p>{{ plant.seedling_frequency }}</p>
              <p>Frequency</p>
            </div>
          </div>
          <div class="page_plant__informations--item">
            <div>
              <i class="icon-sun"></i>
            </div>
            <div>
              <p>{{ plant.seedling_light }}</p>
              <p>Light</p>
            </div>
          </div>
        </div>
        <div class="page_plant__informations--row">
          <p class="page_plant__informations--title">Planting</p>
          <div class="page_plant__informations--item">
            <div>
              <i class="icon-water"></i>
            </div>
            <div>
              <p>{{ plant.planting_frequency }}</p>
              <p>Frequency</p>
            </div>
          </div>
          <div class="page_plant__informations--item">
            <div>
              <i class="icon-sprout"></i>
            </div>
            <div>
              <p>{{ plant.planting_sprouting }}</p>
              <p>Sprouting</p>
            </div>
          </div>
        </div>
      </div>
      <div class="page_plant__localisation">
        <p class="page_plant__informations--title">Localisation</p>
        <p class="page_plant__localisation--text" v-if="plant.localisation">{{ plant.localisation }}</p>
        <p v-else>--- - ----</p>
      </div>
      <p class="page_plant__description">{{ plant.description }}</p>
    </div>
  </section>
</template>

<script>

  import Form_plant from '~/components/form_plant.vue'
  import axios from "../../.nuxt/axios";

  export default {
    components: {
      Form_plant,
    },
    data: function () {
      return {
        formPlant_open: false,
      }
    },
    async asyncData({ $axios, params }) {
      const plant  = await $axios.$get(`http://seeds-api.test/api/plant/${params.id}`);
      return { plant: plant.data };
    },
    methods: {
      showFormPlant: function() {
        this.formPlant_open = !this.formPlant_open;
        console.log()
      },
      async removePlant () {
        let data = {
          'plant_id': this.plant.id,
          'garden_id': 1
        };
        try {
          let res = await this.$axios.post("remove-plant", data);
          return res;
        }
        catch (e) {
          console.log(e)
        }
      }
    }
  }
</script>

<style scoped>

</style>
