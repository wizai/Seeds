<template>
  <div class="block_searchbar">
    <form action="">
      <input type="text" :placeholder="placeholder">
    </form>
  </div>
</template>

<script>
  export default {
    name: "Searchbar",
    props: {
      placeholder: {type: String},
    },
  }
</script>

<style scoped>

</style>
