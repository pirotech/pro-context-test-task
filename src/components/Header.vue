<template>
  <header class="header">
    <h4 class="header__title">Карточки заданий</h4>
    <div class="header-buttons">
      <button
        class="header__create-task"
        @click="onCreateTask"
      >Создать карточку</button>
      <button
        class="header__create-group"
        @click="onCreateGroup"
      >Создать группу</button>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: {
    onCreateTask: Function,
    onCreateGroup: Function
  }
}
</script>

<style scoped lang="scss">
.header {
  display: flex;
  justify-content: space-between;
  padding: 20px;
  background-color: white;
  &__title {
    text-align: left;
  }
  &-buttons {
  }
  &__create-task {
  }
  &__create-group {
    margin-left: 12px;
  }
}
</style>
