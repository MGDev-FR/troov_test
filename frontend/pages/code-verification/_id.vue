<template>
    <div class="container">
        <h1>Réinitilisation du mot de passe</h1>
        <p>Entrez le code de vérification reçu par email</p>
        <b-form>
            <b-form-group
                id="input-group-1"
            >
                <b-form-input
                id="input-1"
                :v-model="code"
                type="text"
                placeholder="Ex.: 000000"
                required
                ></b-form-input>
            </b-form-group>

            <b-button type="button" @click="submitForm(code)" variant="primary">Envoyer</b-button>
        </b-form>
  </div>
</template>

<script>
export default {
    data() {
        return {
            code: ''
        }
    },
    methods: {
        submitForm(code){
            this.$axios.post('/auth/password-verification-code', {code})
                .then(res => {
                    this.$toast.success(res.data.message);
                })
                .catch(err => {
                    console.log(err);
                });
        }
    }
}
</script>
