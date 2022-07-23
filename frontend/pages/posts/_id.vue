<template>
  <div class="container">
    <PostForm submitButton="Modifier" :submitForm="updatePost" :title="title" :content="content" />
  </div>
</template>

<script>
  import PostForm from '@/components/PostForm.vue'

  export default {
    data() {
      return {
        title: '',
        content: '',
        show: true
      }
    },
    components: {
      PostForm
    },
    middleware: "auth",
    mounted() {
        this.$axios.get('/posts/' + this.$route.params.id)
            .then((res) => {
                console.log(res);
                if (res.status === 200){
                    this.title = res.data.title;
                    this.content = res.data.content;
                }
            })
    },
    methods: {
      async updatePost(form) {
        this.$axios.put('/posts/' + this.$route.params.id, {form})
            .then((res) => {
                if (res.status === 200){
                    this.$toast.success(res.data.message);
                    this.$router.push({ path: "/user/my-account" });
                }
            })
      },
    }
  }
</script>