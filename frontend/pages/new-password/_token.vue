<template>
    <div class="container">
        <h1>Modifier votre mot de passe</h1>
        <b-form>
            <b-form-group
                id="input-group-1"
                label="Nouveau mot de passe :"
                label-for="input-1"
            >
                <b-form-input
                id="input-1"
                v-model="password"
                type="password"
                required
                ></b-form-input>
            </b-form-group>

            <b-form-group
                id="input-group-2"
                label="Répétez le mot de passe :"
                label-for="input-2"
            >
                <b-form-input
                id="input-2"
                v-model="password_repeat"
                type="password"
                required
                ></b-form-input>
            </b-form-group>

            <b-button type="button" @click="submitForm(password)" variant="primary">Changer</b-button>
        </b-form>
  </div>
</template>

<script>
export default {
    data() {
        return {
            password: '',
            password_repeat: ''
        }
    },
    methods: {
        submitForm(password){
            if (password != this.password_repeat){
                this.$toast.error('Les mots de passe ne correspondent pas !');
            } else {
                this.$axios.post('/password/change', {
                    password: password, token: this.$route.params.token
                })
                    .then(res => {
                        this.$router.push({name: 'login'});
                        this.$toast.success(res.data.message);
                    })
                    .catch(err => {
                        console.log(err);
                    });
            }
        }
    }
}
</script>
