<template>
  <div class="post">
    <div>
      <div><strong>Название:</strong> {{ post.title }}</div>
      <div><strong>Описание:</strong> {{ post.body }}</div>
    </div>
    <div class="postButtons">
      <my-button @click="$emit('remove', post)">
        Удалить
      </my-button>
    </div>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";

export default {
  components: {MyButton},
  props: {
    post: {
      type: Object,
      required: true
    }
  },
}
</script>

<style scoped>
.post {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}


.postButtons {
  height: 100%;
}

.post {
  padding: 10px;
  border: 2px solid green;
  margin-top: 10px;
}
</style>