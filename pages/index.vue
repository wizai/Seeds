<template>
  <section class="page_login">
    <div class="page_login__logo">
      <logo />
      <Logo_text />
      <p class="page_login__baseline">Gardening is simple</p>
    </div>
    <div class="page_login__actions">
      <nuxt-link to="signup" class="btn">Create an account</nuxt-link>
      <nuxt-link to="login" class="btn btn-light">Login</nuxt-link>
    </div>
  </section>
</template>

<script>
import Logo from '~/components/Logo.vue'
import Logo_text from '~/components/Logo_text.vue'

export default {
  components: {
    Logo,
    Logo_text
  }
}
</script>

<style>

</style>
