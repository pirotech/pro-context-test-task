<template>
  <div v-if="opened" class="modal" @click.self.stop="closeModal">
    <div class="modal-wrapper">
      <h4 class="modal-header">{{title}}</h4>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    opened: Boolean,
    title: String,
    closeModal: Function
  }
}
</script>

<style scoped lang="scss">
.modal {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  min-height: 100vh;
  background-color: rgba(0, 0, 0, .6);
  &-wrapper {
    width: 100%;
    max-width: 500px;
    padding: 20px;
    margin: 0 10px;
    background-color: white;
    border-radius: 2px;
  }
}
</style>
