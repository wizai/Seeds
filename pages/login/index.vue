<template>
  <section class="page_signin">
    <div class="page__header">
      <nuxt-link to="/" class="page__header--link">
        <i class="icon-arrow"></i>
      </nuxt-link>
    </div>
    <div class="page__title">
      <h1>Create an account</h1>
    </div>
    <form method="post" @submit.prevent="login" class="custom_form">
      <div class="custom_form__row" :class="errors && errors.email ? 'error' : ''">
        <input
          type="email"
          id="register_mail"
          name="register_mail"
          required
          v-model="fields.email"
          placeholder=" ">
        <label for="register_mail">E-mail</label>
        <span class="custom_form__row--error" v-if="errors && errors.email">{{ errors.email[0] }}</span>
      </div>
      <div class="custom_form__row" :class="errors && errors.password ? 'error' : ''">
        <input
          type="password"
          id="register_password"
          name="register_password"
          required
          v-model="fields.password"
          placeholder=" ">
        <label for="register_password">Password</label>
        <span class="custom_form__row--error" v-if="errors && errors.password">{{ errors.password[0] }}</span>
      </div>
      <div class="custom_form__actions page__footer">
        <input type="submit" value="Login" class="btn" :disabled="isLoading">
      </div>
    </form>
  </section>
</template>

<script>
  export default {
    name: "signin",
    data() {
      return {
        fields: {
          email: '',
          password: ''
        },
        isLoading: false,
        errors: null
      }
    },
    methods: {
      async login () {
        this.isLoading = true
        this.errors = null
        try {
          await this.$auth.loginWith("local", {
            data: {
              email: this.fields.email,
              password: this.fields.password
            }
          });
          this.$router.push('/garden')
        } catch (e) {
          this.isLoading = false
          this.errors = e.response.data
        }
      }
    }
  }
</script>

<style scoped>

</style>
