<template>
  <div class="container">
    <PostForm submitButton="Publier" :submitForm="sendPost" />
  </div>
</template>

<script>
  import PostForm from '../../components/PostForm.vue'

  export default {
    data() {
      return {
        form: {
          title: '',
          content: ''
        },
        show: true
      }
    },
    components: {
      PostForm
    },
    middleware: "auth",
    methods: {
      async sendPost(form) {
        await this.$axios.post('/posts', form)
        .then((response) => {
          console.log(response);
          if (response.status === 200){
            this.$toast.success(response.data.message);
            this.$router.push({ name: "user/my-account" });
          }
        })
        .catch((err) => {
          console.log(err);
        });
      },
    }
  }
</script>