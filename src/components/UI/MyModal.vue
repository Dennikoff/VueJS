<template>
  <div class="myModal" v-if="show" @click="$emit('visibility',false)">
    <div @click.stop class="dialogContent">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'my-modal',
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  methods: {

  }
}
</script>

<style scoped>
.myModal {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  background: rgba(0,0,0,0.4);
  display: flex;
}

.dialogContent {
  margin: auto;
  background: white;
  border: 2px solid teal;
  border-radius: 3vw;
  padding: 20px;
}

</style>