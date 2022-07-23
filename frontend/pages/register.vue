<template>
    <div class="container">
        <h1>Inscription</h1>
        <UserAuthForm buttonText="S'inscrire" :submitForm="registerUser" />
    </div>
</template>

<script>
import UserAuthForm from '@/components/UserAuthForm'
export default {
    components: {
        UserAuthForm
    },
    methods: {
        async registerUser(registrationInfo){
            await this.$axios.post('/auth/signup', registrationInfo);
            this.$auth.loginWith('local', {
                data: registrationInfo
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
