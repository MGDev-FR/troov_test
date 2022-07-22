<template>
    <div class="container">
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
    }
}
</script>

<style lang="scss" scoped>

</style>
