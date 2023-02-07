<template>
  <form @submit.prevent>
    <h4>Создать пост</h4>
    <my-input
        v-model:value="post.title"
        type="text"
        placeholder="Название поста"
    />
    <my-input
        v-model:value="post.body"
        type="text"
        placeholder="Описание поста"
    />
    <my-button
        style="align-self: flex-end; margin-top: 15px"
        @click="createPost"
    >Создать пост</my-button>
  </form>
</template>

<script>




export default {
  data() {
    return {
      post: {
        title: '',
        body: '',
      },
    }
  },
  methods: {
    createPost(){
      this.post.id = Date.now()
      this.$emit('create', this.post)
      this.post = {
        id: '',
        title: '',
        body: '',
      };
    },
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}


</style>