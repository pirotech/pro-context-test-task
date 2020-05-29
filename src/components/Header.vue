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
  @media (max-width: 720px) {
    flex-direction: column;
    align-items: center;
  }
  &__title {
    text-align: left;
    @media (max-width: 720px) {
      text-align: center;
    }
  }
  &-buttons {
    @media (max-width: 720px) {
      margin-top: 12px;
    }
    @media (max-width: 375px) {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
  }
  &__create-task {
  }
  &__create-group {
    margin-left: 12px;
    @media (max-width: 375px) {
      margin-left: 0;
      margin-top: 8px;
    }
  }
}
</style>
