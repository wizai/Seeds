<template>
  <section class="page_signup">
    <div class="page__header">
      <nuxt-link to="/" class="page__header--link">
        <i class="icon-arrow"></i>
      </nuxt-link>
    </div>
    <div class="page__title">
      <h1>Create an account</h1>
    </div>
    <form method="post" @submit.prevent="register" class="custom_form">
      <div class="custom_form__row">
        <input
          type="text"
          id="register_firstname"
          name="register_firstname"
          v-model="firstname"
          required
          placeholder=" ">
        <label for="register_firstname">First name</label>
        <span class="custom_form__row--error">Invalid email address</span>
      </div>
      <div class="custom_form__row">
        <input
          type="text"
          id="register_lastname"
          name="register_lastname"
          v-model="lastname"
          required
          placeholder=" ">
        <label for="register_lastname">Last name</label>
        <span class="custom_form__row--error">Invalid email address</span>
      </div>
      <div class="custom_form__row">
        <input
          type="email"
          id="register_mail"
          name="register_mail"
          v-model="email"
          required
          placeholder=" ">
        <label for="register_mail">E-mail</label>
        <span class="custom_form__row--error">Invalid email address</span>
      </div>
      <div class="custom_form__row">
        <input
          type="password"
          id="register_password"
          name="register_password"
          v-model="password"
          required
          placeholder=" ">
        <label for="register_password">Password</label>
        <span class="custom_form__row--error">Incorrect password</span>
      </div>
      <div class="custom_form__actions page__footer">
        <input type="submit" value="Register" class="btn">
      </div>
    </form>
  </section>
</template>

<script>
  export default {
    name: "signup",
    data() {
      return {
        firstname: '',
        lastname: '',
        email: '',
        password: '',
        error: null
      }
    },
    methods: {
      async register() {
        try {
          await this.$axios.post('auth/register', {
            firstname: this.firstname,
            lastname: this.lastname,
            email: this.email,
            password: this.password
          });

          await this.$auth.loginWith('local', {
            data: {
              email: this.email,
              password: this.password
            },
          });

          this.$router.push('garden')
        } catch (e) {
          this.error = e.response.data.message
        }
      }
    }
  }
</script>

<style scoped>

</style>
