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
    <form action="" class="custom_form">
      <div class="custom_form__row">
        <input
          type="text"
          id="register_firstname"
          name="register_firstname"
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
          required
          placeholder=" ">
        <label for="register_password">Password</label>
        <span class="custom_form__row--error">Incorrect password</span>
      </div>
      <div class="custom_form__row">
        <input
          type="password"
          id="register_repeatPassword"
          name="register_repeatPassword"
          required
          placeholder=" ">
        <label for="register_repeatPassword">Confirm password</label>
        <span class="custom_form__row--error">Password must match</span>
      </div>
      <div class="custom_form__actions page__footer">
        <input type="submit" value="Register" class="btn" >
      </div>
    </form>
  </section>
</template>

<script>
    export default {
        name: "signup"
    }
</script>

<style scoped>

</style>
