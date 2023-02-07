<template>
  <div class="app">
    <post-form
        @create="createPost"
    />
    <post-list
        :posts="posts"
        @remove="remove"
    />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";

export default {
  components: {
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
      ]
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
    },
    remove(post) {
      console.log(post)
      this.posts = this.posts.filter(value => value.id !== post.id)
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
