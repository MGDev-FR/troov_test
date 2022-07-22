<template>
    <div class="container">

        <div class="row">
            <div class="col">
                <b-link to="/user/my-account"><b-icon-arrow-left></b-icon-arrow-left> Retour à la liste des articles</b-link>
            </div>
            <div class="col text-end">
                <router-link v-if="post.userId == $auth.user._id" :to="{ name: 'posts-id', params: {id: post._id} }"><b-icon-pencil></b-icon-pencil></router-link>
                <b-icon-trash v-if="post.userId == $auth.user._id" v-b-modal.remove-post-confirm></b-icon-trash>
            </div>
        </div>

        <div class="row">
            <div class="col text-center">
                <h1>{{ post.title }}</h1>
            </div>
        </div>

        <div class="row">
            <div class="col">
                <p>{{ post.content }}</p>
            </div>
        </div>

    </div>
</template>

<script>
export default {
    data(){
        return {
            post: {}
        }
    },
    middleware: "auth",
    mounted(){
        this.$axios.get('/posts/' + this.$route.params.id)
            .then(res => {
                if (res.status === 200 || res.status === 201){
                    this.post = res.data;
                }
            })
            .catch(err => {
                console.log(err);
            });
    }
}
</script>
