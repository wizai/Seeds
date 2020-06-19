<template>
    <p class="SeedsLogo_text">Seeds</p>
</template>

<script>
    export default {
        name: "Logo_text"
    }
</script>

<style lang="scss" scoped>

  @import "@/assets/scss/style.scss";

  .SeedsLogo_text{
    font-size: 5rem;
    position: relative;
    padding-right: 15px;
    font-weight: 900;
    display: inline-block;
    &:after{
      content: '.';
      color: $green;
      position: absolute;
      bottom: 0px;
      right: 0;
    }
  }

</style>
