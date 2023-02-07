<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <div class="appButtons">
      <my-button
          @click="() => {this.modalVisible = true}">Создать пост
      </my-button>
      <my-select
        v-model="selectedSort"
        :options="sortOptions"
      />
    </div>
    <my-modal
        v-model:show="modalVisible"
        @visibility="changeVisibility"
    >
      <post-form
          @create="createPost"
      />
    </my-modal>
    <post-list
        :posts="posts"
        @remove="remove"
        v-if="!isPostsLoading"
    />
    <div v-else>ЗАГРУЗКА</div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import MyModal from "@/components/UI/MyModal.vue";
import MyButton from "@/components/UI/MyButton.vue";
import axios from "axios";
import MySelect from "@/components/UI/MySelect.vue";

export default {
  components: {
    MySelect,
    MyButton,
    MyModal,
    PostForm,
    PostList
  },
  data() {
    return {
      posts: [],
      modalVisible: false,
      isPostsLoading: false,
      selectedSort: '',
      sortOptions: [
        {value: 'title', name: 'По названию'},
        {value: 'body', name: 'По описанию'},
      ]
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
    },
    async fetchPosts() {
      let url = 'https://jsonplaceholder.typicode.com/posts?_limit=20'
      try {
        this.isPostsLoading = true
        setTimeout(async () => {
              let response = await axios.get(url)
              this.posts = response.data
              this.isPostsLoading = false
            }, 1000
        )
      } catch (e) {
        console.log('here')
        console.log(e)
      } finally {

      }
    }
  },
  mounted() {
    this.fetchPosts()
  },
  watch: {
    selectedSort(newValue) {
      console.log(newValue)
      console.log(this.selectedSort)
      console.log(this.posts)
      this.posts.sort((a, b) => {
        return a[newValue]?.localeCompare(b[newValue])
      })
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

.appButtons{
  display: flex;
  justify-content: space-between;
}
</style>
