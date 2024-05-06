<template>
  <div
    class="base-text-field"
    :class="classes"
  >
    <input
      v-model="value"
      :id="id"
      class="base-text-field__input"
      :type="type"
      @focusin="focusin"
      @focusout="focusout"
    >
    <label
      v-if="label"
      :for="id"
      class="base-text-field__label"
    >
      {{ label }}
      <span
        v-if="required"
        class="base-text-field__required"
      >
        *
      </span>
    </label>
    <div
      v-if="isError && error"
      class="base-text-field__error"
    >
      <p>{{ error }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'base-text-field',
  model: {
    prop: 'value',
    event: 'input',
  },
  props: {
    value: { type: String, default: '' },
    label: { type: String, default: '' },
    type: { type: String, default: 'text' },
    isError: { type: Boolean, default: false },
    error: { type: String, default: '' },
    required: { type: Boolean, default: false },
    // withFiles: { type: Boolean, default: false },
  },
  data () {
    return {
      id: null,
      focused: false,
    };
  },
  computed: {
    classes () {
      return {
        'base-text-field--error': this.isError,
        'base-text-field--filled': this.value && this.value.length,
        'base-text-field--focused': this.focused,
      };
    },
  },
  created () {
    this.id = `${Math.random(1000)}-${this.type}`;
  },
  methods: {
    focusin (event) {
      this.focused = true;
      this.$emit('focusin', event);
    },
    focusout (event) {
      this.focused = false;
      this.$emit('focusout', event);
    },
  },
};
</script>

<style lang="scss" scoped>
.base-text-field {
  position: relative;
  padding: $field-padding;

  font-family: inherit;
  color: $text-color;
  transition: $transition;

  &__label {
    position: absolute;
    top: 4px;
    left: 0;
    color: inherit;
    font-size: inherit;
    font-weight: inherit;
    transition: $transition;
  }

  &__input {
  }

  &:after {
    content: '';
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 1px;
    background: $placeholder-color;
    transition: $transition;
  }

  &--filled {
    .base-text-field__label {
      top: -3px;
      transform: translateY(-50%);
      font-size: 0.8em;
    }
  }

  &--focused {
    .base-text-field__label {
      top: -4px;
      transform: translateY(-50%);
      font-size: 0.8em;
    }

    &::after {
      background: $main-color;
    }
  }

  &--error {

  }
}
</style>
