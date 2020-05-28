<template>
  <label class="ui-radio-button">
    <input
      type="radio"
      class="ui-radio-button__input"
      :name="name"
      :value="value"
      :checked="checked"
      @change="onRadioChange"
    />
    <i
      class="ui-radio-button__icon"
    ><i></i></i>
    <span class="ui-radio-button__label">{{label}}</span>
  </label>
</template>

<script>
export default {
  name: "UiRadioButton",
  props: {
    label: String,
    name: String,
    value: Number,
    checked: Boolean,
    onChange: Function
  },
  methods: {
    onRadioChange(e) {
      const { name } = e.target;
      this.onChange(name, this.value);
    }
  }
}
</script>

<style scoped lang="scss">
.ui-radio-button {
  display: flex;
  align-items: center;
  &__input {
    display: none;
    &:checked ~ .ui-radio-button__icon {
      display: flex;
      justify-content: center;
      align-items: center;
      i {
        display: inline-block;
        min-width: 12px;
        height: 12px;
        border-radius: 50%;
        background-color: #888;
      }
    }
  }
  &__icon {
    display: inline-block;
    min-width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: white;
    border: 2px solid #777;
    cursor: pointer;
  }
  &__label {
    margin-left: 8px;
  }
}
</style>
