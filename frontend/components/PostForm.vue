<template>
    <b-form v-if="show">
      <b-form-group
        label="Titre :"
        label-for="title"
      >
        <b-form-input
          id="title"
          :v-model="form.title"
          type="text"
          placeholder="Titre de l'article"
          required
          :value="form.title"
        ></b-form-input>
      </b-form-group>

      <b-form-group 
        label="Article :" 
        label-for="content"
      >
        <b-form-textarea
          id="content"
          :v-model="form.content"
          placeholder="Écrivez votre article ici..."
          required
          :value="form.content"
        ></b-form-textarea>
      </b-form-group>

      <b-button type="button" @click="submitForm(form)" variant="primary">{{ submitButton }}</b-button>
    </b-form>
</template>

<script>
export default {
    data() {
        return {
            form: {
                title: this.title ? this.title : '',
                content: this.content ? this.content : '',
            },
            show: true
        }
    },
    props: ["submitButton", "submitForm", "title", "content"]
}
</script>
