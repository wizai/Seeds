<template>
  <div id="root">
    <div class="App">
      <div class="container">
        <nuxt />
      </div>
    </div>
  </div>
</template>
<script>
  import { mapGetters } from 'vuex'

  export default {
    computed: {
      ...mapGetters(['isAuthenticated', 'loggedInUser'])
    },
    methods: {
      async logout() {
        await this.$auth.logout().then(() => {
          console.log('Vous êtes desormais déconnecté(e)')
        })
      }
    }
  }
</script>
