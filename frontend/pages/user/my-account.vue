<template>
  <div class="container">
    <div class="row mb-3">
      <div class="col text-center">
        <b-button variant="primary" to="/posts/add-post"><b-icon-plus-circle></b-icon-plus-circle> Créer un article</b-button>
      </div>
    </div>
    <div class="row">
      <div class="col-md-6 col-sm-12" v-for="post in posts" :key="post._id">

        <b-modal :id="'remove-post-confirm-' + post._id">
            <h4 class="my-4">Êtes-vous sûr(e) de vouloir supprimer cet article ?</h4>
            <template #modal-footer>
              <b-button class="mt-3" @click="$bvModal.hide('remove-post-confirm-' + post._id);removePost(post._id)" variant="primary">Oui</b-button>
            <b-button class="mt-3" @click="$bvModal.hide('remove-post-confirm-' + post._id)" variant="secondary">Non</b-button>
            </template>
        </b-modal>

        <b-card
          :id="'bcard-' + post._id"
          :title="post.title"
          tag="article"
          style="max-width: 20rem;"
          class="mb-2 mt-2 b-card-post"
        >
          <div class="edit-functions">
            <router-link v-if="post.userId == $auth.user._id" :to="{ name: 'posts-id', params: {id: post._id} }"><b-icon-pencil></b-icon-pencil></router-link>
            <b-icon-trash v-if="post.userId == $auth.user._id" @click="$bvModal.show('remove-post-confirm-' + post._id)"></b-icon-trash>
          </div>
          <b-card-text>
            {{ post.content.substr(0, 100) }} ...
          </b-card-text>

          <b-card-text>
            <div class="row">
              <div class="col text-center">
                <b-icon-hand-thumbs-up-fill @click="addLike(post._id, 1)" v-if="includes(post.usersLiked, $auth.user._id)"></b-icon-hand-thumbs-up-fill> 
                <b-icon-hand-thumbs-up @click="addLike(post._id, 1)" v-else></b-icon-hand-thumbs-up> 
                {{ post.likes }}
              </div>
              <div class="col text-center">
                <b-icon-hand-thumbs-down-fill @click="addLike(post._id, -1)" v-if="includes(post.usersDisliked, $auth.user._id)"></b-icon-hand-thumbs-down-fill> 
                <b-icon-hand-thumbs-down @click="addLike(post._id, -1)" v-else></b-icon-hand-thumbs-down>
                {{ post.dislikes }}
              </div>
            </div>
          </b-card-text>

          <div class="row">
            <div class="col text-center">
              <b-button :to="{ name: 'show-post-id', params: {id: post._id} }" variant="primary">Lire la suite</b-button>
            </div>
          </div>
        </b-card>
      </div>
    </div>
  </div>
</template>

<script>
  import { includes } from 'lodash';
  export default {
    data() {
      return {
        posts: [],
        includes: includes,
      }
    },
    middleware: "auth",
    mounted() {
      this.getAllPosts();
    },
    methods: {
      async addLike(postId, likeType){
        await this.$axios.post('/posts/'+postId+'/like', {
          like: likeType
        })
          .then(res => {
            this.getAllPosts();
            if (res.data.type === 'danger'){
              this.$toast.error(res.data.message);
            } else {
              this.$toast.success(res.data.message);
            }
            
          })
          .catch(err => {
            console.log(err);
          });
      },
      async getAllPosts(){
        await this.$axios.get('/posts')
        .then(res => {
          this.posts = res.data;
        });
      },
      removePost(postId){
        this.$axios.delete('/posts/' + postId)
        .then(res => {
          document.getElementById('bcard-'+postId).style.display = 'none';
          this.$toast.success(res.data.message);
        });
      }
    }
  }
</script>

<style scoped>
.b-card-post {
  position: relative;
}
.edit-functions {
  position: absolute;
  top: 5px;
  right: 10px;
}
</style>