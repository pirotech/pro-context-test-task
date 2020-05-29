<template>
  <div class="ui-task">
    <h5 class="ui-task__name">{{value.name}}</h5>
    <div class="ui-task-buttons">
      <button
        class="button_danger ui-task__delete"
        @click="onRemove(value)"
      >Удалить</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "UiGroup",
  props: {
    value: Object,
    onRemove: Function
  }
}
</script>

<style scoped lang="scss">
.ui-task {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  min-width: 300px;
  max-width: 300px;
  padding: 20px;
  background-color: white;
  border-radius: 2px;
  @media (max-width: 576px) {
    min-width: 280px;
    max-width: 280px;
  }
  &__name {
    width: 100%;
    text-align: left;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  &-buttons {
    margin-top: 12px;
  }
  &__delete {
  }
}
</style>
