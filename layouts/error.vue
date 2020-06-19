<template>
  <section class="page_404">
    <h1>404</h1>
    <h2>Oops! This page cannot be found.</h2>
    <p>There's nothing here.</p>
    <nuxt-link to="/" class="btn">Go back to homepage</nuxt-link>
  </section>
</template>

<script>
  export default {
    props: ['error'],
    layout: 'errorlayout',

  }
</script>

<style lang="scss" scoped>

</style>
