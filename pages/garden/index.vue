<template>
  <section class="page_garden">
    <div class="page__header">
      <nuxt-link to="profil" class="page__header--user">
        <logo />
      </nuxt-link>
      <h1>Hi, {{this.$auth.user.firstname}} !</h1>
      <nuxt-link to="search" class="page__header--add">+</nuxt-link>
    </div>
    <div class="block_searchbar">
      <form action="">
        <input type="text" placeholder="Search your seed" @keyup="research($event.target.value)">
      </form>
    </div>
    <div class="block_filters">
      <ul class="block_filters--list">
        <li class="block_filters--item Fruit"
            @click="filter('.Fruit')"
            data-filter=".Fruit">
          <div>
            <i class="icon-fruits"></i>
            <span>Fruits</span>
          </div>
        </li>
        <li class="block_filters--item Vegetable"
            @click="filter('.Vegetable')"
            data-filter=".Vegetable">
          <div>
            <i class="icon-vegetable"></i>
            <span>Vegetables</span>
          </div>
        </li>
        <li class="block_filters--item Plant"
            @click="filter('.Plant')"
            data-filter=".Plant">
          <div>
            <i class="icon-plants"></i>
            <span>Plants</span>
          </div>
        </li>
        <li class="block_filters--item Aromatic"
            @click="filter('.Aromatic')"
            data-filter=".Aromatic">
          <div>
            <i class="icon-aromatic"></i>
            <span>Aromatics</span>
          </div>
        </li>
      </ul>
    </div>
    <div class="page_garden__content">
      <nuxt-link :to="{name: 'plant-id', params: { id: item.id } }" :class="'block_seed ' + item.category" v-for="item in getAllPlantInGarden" :key="item.id">
        <div class="block_seed--img"
             :style="{ 'background-image': 'url(' + item.image + ')' }">
        </div>
        <div class="block_seed--text">
          <p class="block_seed--title">{{ item.title }}</p>
          <p class="block_seed--category">{{ item.category }}</p>
          <p class="block_seed--date" v-if="item.sowed">Sowed : {{ item.sowed | moment('MMM d, YYYY') }}</p>
          <p class="block_seed--date" v-if="item.planted">Planted : {{ item.planted | moment('MMM d, YYYY') }}</p>
        </div>
      </nuxt-link>
      <!--<div class="block_seed">
        <div class="block-infos">
          <p>You have no fruit <br> <b>You can add them by doing a search.</b></p>
          <span class="btn">Start research</span>
        </div>
      </div>-->
    </div>
  </section>
</template>

<script>

  import Logo from '~/components/Logo.vue'
  import { mapGetters } from 'vuex'

  let Isotope;
  let qsRegex;
  let buttonFilter;

  if (process.browser) {
    Isotope = require("isotope-layout");
  }

    export default {
      name: "garden",
      data: function () {
        return {
          formPlant_open: false,
          gardens: {}
        }
      },
      components: {
        Logo,
      },
      async asyncData({ $axios }) {
        const gardens = await $axios.$get(`http://seeds-api.test/api/garden`);
        return {  gardens: gardens };
      },
      mounted() {
        this.isotope();
        this.user = this.$auth.user.id

      },
      computed: {
        ...mapGetters(['isAuthenticated', 'loggedInUser']),

        getAllPlantInGarden: function () {
          console.log(this.gardens.filter(x => x.user_id === this.$auth.user.id));
          const garden =  this.gardens.filter(x => x.user_id === this.$auth.user.id);
          return garden[0].plants ;
        },
      },
      methods: {
        isotope() {
          this.iso = new Isotope(".page_garden__content", {
            itemSelector: ".block_seed",
            percentPosition: true,
            getSortData: {
              category: '.block_seed--title'
            },
            sortBy : 'category',
            filter: function(e) {
              let _this = e;
              let searchResult = qsRegex ? $(_this).text().match( qsRegex ) : true;
              let buttonResult = buttonFilter ? $(_this).is( buttonFilter ) : true;
              return searchResult && buttonResult;
            }
          });
          this.iso.layout();
        },
        debounce: function(fn, threshold) {
          let timeout;
          threshold = threshold || 100;
          return function debounced() {
            clearTimeout( timeout );
            let args = arguments;
            let _this = this;
            function delayed() {
              fn.apply( _this, args );
            }
            timeout = setTimeout( delayed, threshold );
          };
        },
        filter: function(slug) {
          let oldActive = $(".block_filters--list .active").first();
          if (slug === oldActive.data("filter")) {
            slug = "*";
          } else {
            let currentActive = $(".block_filters--item" + slug).first();
            currentActive.addClass("active");
          }
          buttonFilter = slug;
          oldActive.removeClass("active");
          this.iso.arrange();
        },
        research: function (event) {
          let _this = this;
          (_this.debounce( function() {
            qsRegex = new RegExp( event, 'gi' );
            _this.iso.arrange();
          }, 200 ))();
        }
      },
      middleware: 'auth'
    }
</script>

<style scoped>

</style>
