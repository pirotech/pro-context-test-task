<template>
  <label class="ui-checkbox" @click="onChange">
    <i
      class="ui-checkbox__icon"
      :class="{'ui-checkbox__icon_checked': value}"
    ><i></i></i>
    <span class="ui-checkbox__label">{{label}}</span>
  </label>
</template>

<script>
export default {
  name: "UiCheckbox",
  props: {
    label: String,
    value: Boolean,
    onChange: Function
  }
}
</script>

<style scoped lang="scss">
.ui-checkbox {
  display: flex;
  align-items: center;
  &__icon {
    display: inline-block;
    min-width: 20px;
    height: 20px;
    border-radius: 2px;
    background-color: white;
    border: 2px solid #777;
    cursor: pointer;
    &_checked {
      display: flex;
      justify-content: center;
      align-items: center;
      i {
        display: inline-block;
        min-width: 12px;
        height: 12px;
        background-color: #888;
      }
    }
  }
  &__label {
    margin-left: 8px;
  }
}
</style>
