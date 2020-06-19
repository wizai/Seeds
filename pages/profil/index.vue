<template>
    <section class="page_profil">
      <div class="page__header">
        <nuxt-link to="garden" class="page__header--link">
          <i class="icon-arrow"></i>
        </nuxt-link>
      </div>
      <div class="page__title">
        <h2>My profil</h2>
      </div>
      <div class="page_profil__user">
        <p class="page_profil__user--firstname">Firstname </p>
        <p class="page_profil__user--lastname">lastname</p>
        <p class="page_profil__user--email">email</p>
        <span class="page_profil__user--logout" @click="logout">Logout</span>
      </div>
    </section>
</template>

<script>

  import { mapGetters } from 'vuex'

  export default {
    name: 'profil',
    computed: {
      ...mapGetters(['isAuthenticated', 'loggedInUser'])
    },
    methods: {
      async logout() {
        await this.$auth.logout();
        this.$router.push('/')
      }
    }
  }
</script>

<style scoped>

</style>
