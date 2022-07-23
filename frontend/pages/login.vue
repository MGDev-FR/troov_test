<template>
    <div class="container">
        <h1>Connexion</h1>
        <UserAuthForm buttonText="Se connecter" :submitForm="loginUser" :showPasswordReset="true" />
    </div>
</template>

<script>
import UserAuthForm from '@/components/UserAuthForm'
export default {
    components: {
        UserAuthForm
    },
    methods: {
        loginUser(loginInfo){
            this.$auth.loginWith('local', {data: loginInfo})
                .then(res => {
                    console.log(res);
                })
                .catch(err => {
                    this.$toast.error("Le mot de passe et/ou l'email sont incorrects !");
                });
        }
    },
    mounted() {
        if (this.$auth.loggedIn){
            this.$router.push({path: '/user/my-account'});
        }
    }
}
</script>
