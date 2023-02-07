<template>
  <input :value="value" @input="updateInput" class="input" type="text">
</template>

<script>
export default {
  name: 'my-input',
  props: {
    value: [String, Number]
  },
  methods: {
    updateInput(event) {
      this.$emit('update:value', event.target.value)
    }
  }
}
</script>

<style scoped>
.input {
  width:100%;
  padding: 5px 10px;
  margin-top: 10px;
  border: 1px solid teal;
}
</style>