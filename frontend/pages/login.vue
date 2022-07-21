<template>
    <div class="container">
        <UserAuthForm buttonText="Se connecter" :submitForm="loginUser" />
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
            this.$auth.loginWith('local', {
                data: loginInfo
            })
        }
    }
}
</script>
