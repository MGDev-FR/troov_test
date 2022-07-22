<template>
  <div class="container">
    <b-form v-if="show">
      <b-form-group
        id="input-group-1"
        label="Email :"
        label-for="input-1"
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          placeholder="Ex.: contact@michael-godinhodacosta.fr"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Mot de passe :" label-for="input-2">
        <b-form-input
          id="input-2"
          type="password"
          v-model="form.password"
          placeholder="Ex.: MySuperMegaPasswordSecure2022"
          required
        ></b-form-input>
        <b-link to="/password-reset" v-if="showPasswordReset">Mot de passe oublié ?</b-link>
      </b-form-group>

      <b-button type="button" @click="submitForm(form)" variant="primary">{{ buttonText }}</b-button>
    </b-form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          email: '',
          password: '',
        },
        show: true
      }
    },
    props: ["buttonText", "submitForm", "showPasswordReset"]
  }
</script>
