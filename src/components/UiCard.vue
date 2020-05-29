<template>
  <div class="ui-card">
    <h5 class="ui-card__name">{{value.name}}</h5>
    <p class="ui-card__status">
      <strong>Статус: </strong>
      <span v-if="value.done" class="_done">Выполнено</span>
      <span v-if="!value.done">Не выполнено</span>
    </p>
    <p class="ui-card__group"><strong>Группа: </strong>{{value.group.name}}</p>
    <div class="ui-card-buttons">
      <button
        class="ui-card__edit"
        @click="onEdit(value)"
      >Редактировать</button>
      <button
        class="button_danger ui-card__delete"
        @click="onRemove(value)"
      >Удалить</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "UiCard",
  props: {
    value: Object,
    onEdit: Function,
    onRemove: Function
  }
}
</script>

<style scoped lang="scss">
.ui-card {
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
  &_button {
    align-items: center;
  }
  &__name {
    width: 100%;
    text-align: left;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  &__status {
    margin-top: 12px;
    ._done {
      color: #228c22;
    }
  }
  &-buttons {
    margin-top: 12px;
  }
  &__edit {
  }
  &__delete {
    margin-left: 12px;
  }
}
</style>
