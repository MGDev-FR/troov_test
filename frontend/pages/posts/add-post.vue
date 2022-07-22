<template>
  <div class="container">
    <PostForm submitButton="Publier" :submitForm="sendPost" />
  </div>
</template>

<script>
  import PostForm from '@/components/PostForm.vue'

  export default {
    components: {
      PostForm
    },
    middleware: "auth",
    methods: {
      async sendPost(form) {
        await this.$axios.post('/posts', form)
        .then((res) => {
          if (res.status === 200){
            this.$toast.success(res.data.message);
            this.$router.push({ path: "/user/my-account" });
          }
        })
        .catch((err) => {
          console.log(err);
        });
      },
    }
  }
</script>