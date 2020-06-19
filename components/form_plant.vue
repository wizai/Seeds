<template>
  <div class="form_addToGarden" :class="{ open: open }">
    <div class="form_addToGarden__container">
      <h1>Add to garden</h1>
      <span class="form_addToGarden__close" @click="hideForm()">&#10005;</span>
      <form action="" class="custom_form">
        <div class="custom_form__row">
          <input
            type="date"
            id="sowing_date"
            name="sowing_date"
            required
            placeholder=" ">
          <label for="sowing_date">Sowing date</label>
          <span class="custom_form__row--error">Invalid date</span>
        </div>
        <div class="custom_form__row">
          <input
            type="date"
            id="planting_date"
            name="planting_date"
            required
            placeholder=" ">
          <label for="planting_date">Planting date</label>
          <span class="custom_form__row--error">Incorrect date</span>
        </div>
        <div class="custom_form__actions">
          <input type="reset" value="Reset" class="btn btn-light">
          <input type="submit" value="Search" class="btn">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
  export default {
    name: "form_plant",
    props: {
      open: {
        type: Boolean
      },
    },
    data() {
      return {
        contactForm: {
          sowing_date: "",
          planting_date: "",
        },
      };
    },
    methods: {
      hideForm (event) {
        this.$emit('hideForm', true)
      }
    }
  }
</script>

<style scoped>

</style>
