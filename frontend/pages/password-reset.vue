<template>
    <div class="container">
        <h1>Demande de réinitialisation du mot de passe</h1>
        <b-form>
            <b-form-group
                id="input-group-1"
                label="Email :"
                label-for="input-1"
            >
                <b-form-input
                id="input-1"
                v-model="email"
                type="email"
                placeholder="Ex.: contact@michael-godinhodacosta.fr"
                required
                ></b-form-input>
            </b-form-group>

            <b-button type="button" @click="submitForm(email)" variant="primary">Demander</b-button>
        </b-form>
  </div>
</template>

<script>
export default {
    data() {
        return {
            email: ''
        }
    },
    methods: {
        submitForm(email){
            this.$axios.post('/auth/password-reset', {email})
                .then(res => {
                    this.$router.push({ name: 'code-verification-id', params: {id: res.data.userId}})
                    this.$toast.success(res.data.message);
                })
                .catch(err => {

                });
        }
    }
}
</script>
