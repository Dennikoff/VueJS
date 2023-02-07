<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <my-button
        @click="() => {this.modalVisible = true}">Создать пост</my-button>
    <my-modal v-model:show="modalVisible" @visibility="changeVisibility">
      <post-form
        @create="createPost"
      />
    </my-modal>
    <post-list
        :posts="posts"
        @remove="remove"
    />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import MyModal from "@/components/UI/MyModal.vue";
import MyButton from "@/components/UI/MyButton.vue";

export default {
  components: {
    MyButton,
    MyModal,
    PostForm,
    PostList
  },
  data() {
    return {
      posts: [
        {id: 1, title: "Пост о JavaScript", body: "JavaScript топ"},
        {id: 2, title: "Пост о kEK", body: "kek топ"},
        {id: 3, title: "Пост о LOL", body: "lol топ"},
        {id: 4, title: "Пост о Orbidol", body: "Orbidol топ"},
      ],
      modalVisible: false
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
      this.modalVisible = false
    },
    remove(post) {
      console.log(post)
      this.posts = this.posts.filter(value => value.id !== post.id)
    },
    changeVisibility(flag) {
      this.modalVisible = flag
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  margin: 10px 15px
}


</style>
