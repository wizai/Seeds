<template>
  <div class="form_addToGarden" :class="{ open: open }">
    <div class="form_addToGarden__container">
      <h1>Add to garden</h1>
      <span class="form_addToGarden__close" @click="hideForm()">&#10005;</span>
      <form action="" class="custom_form" @submit.prevent="addPlant">
        <div class="custom_form__row">
          <input
            type="date"
            id="sowing_date"
            name="sowing_date"
            v-model="formPlant.sowing_date"
            placeholder=" ">
          <label for="sowing_date">Sowing date</label>
          <span class="custom_form__row--error">Invalid date</span>
        </div>
        <div class="custom_form__row">
          <input
            type="date"
            id="planting_date"
            name="planting_date"
            v-model="formPlant.planting_date"
            placeholder=" ">
          <label for="planting_date">Planting date</label>
          <span class="custom_form__row--error">Incorrect date</span>
        </div>
        <div class="custom_form__row">
          <textarea
            id="localisation"
            name="planting_date"
            cols="30" rows="3"
            v-model="formPlant.localisation"
            placeholder=" ">
          </textarea>
          <label for="planting_date">Localisation</label>
        </div>

        <div class="custom_form__actions">
          <input type="reset" value="Reset" class="btn btn-light">
          <input type="submit" value="Add" class="btn">
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
      plant_id: {
        type: Number
      }
    },
    data() {
      return {
        formPlant: {
          sowing_date: '',
          planting_date: '',
          localisation: '',
          plant_id: this.plant_id,
          garden_id: '1'
        },
      };
    },
    methods: {
      hideForm (event) {
        this.$emit('hideForm', true)
      },
      async addPlant () {
        let data = this.formPlant;
        try {
          let res = await this.$axios.post("add-plant", data);
          this.hideForm();
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
