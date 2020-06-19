<template>
  <div id="root">
    <div class="App">
      <div class="container">
        <nuxt/>
      </div>
    </div>
  </div>
</template>

<script>

  export default {
    layoutTransition: {
      name: 'layout',
      mode: 'out-in'
    }
  }
</script>

<style>
  .layout-enter-active, .layout-leave-active {
    transition:all .5s cubic-bezier(.55,0,.1,1);
  }
  .layout-enter, .layout-leave-active {
    opacity: 0
  }
</style>
