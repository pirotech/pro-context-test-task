<template>
  <label class="ui-text-field">
    <span v-if="label" class="ui-text-field__label">{{label}}</span>
    <input
      class="ui-text-field__input"
      type="text"
      :value="value"
      :placeholder="placeholder"
      @input="onChange"
    />
    <span class="ui-text-field__error">{{error}}</span>
  </label>
</template>

<script>
export default {
  name: 'UiTextField',
  props: {
    label: String,
    value: String,
    error: String,
    placeholder: String,
    onChange: Function
  }
}
</script>

<style scoped lang="scss">
.ui-text-field {
  display: flex;
  flex-direction: column;
  &__label {
    display: block;
    font-size: 14px;
    text-align: left;
    color: #333333;
  }
  &__input {
    width: 100%;
    margin-top: 4px;
  }
  &__error {
    display: block;
    min-width: 1px;
    min-height: 14px;
    margin-top: 2px;
    font-size: 12px;
    text-align: left;
    color: #d45;
  }
}
</style>
