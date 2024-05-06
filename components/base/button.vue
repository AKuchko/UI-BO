<template>
  <button
    class="base-button"
    :class="classes"
  >
    <div
      v-if="isBefore"
      class="base-button__before"
    >
      <slot name="before">
        <component :is="icon" />
      </slot>
    </div>
    <slot>
      <span
        v-if="title"
        class="base-button__title"
      >
        {{ title }}
      </span>
    </slot>
  </button>
</template>

<script>
export default {
  name: 'base-button',
  props: {
    title: { type: String, default: '' },
    icon: { type: String, default: '' },
    disabled: { type: Boolean, default: false },
    outlined: { type: Boolean, default: false },
    small: { type: Boolean, default: false },
    rounded: { type: Boolean, default: false },
  },
  computed: {
    isBefore () {
      return !!this.icon || !!this.$slots.before;
    },
    classes () {
      return {
        'base-button--outline': this.outlined,
        'base-button--disabled': this.disabled,
        'base-button--small': this.small,
        'base-button--rounded': this.rounded,
      };
    },
  },
};
</script>

<style lang="scss">
.base-button {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;

  padding: $button-padding;
  border-radius: $button-border-radius;
  color: $contrast-color;
  background: $main-color;
  transition: $transition;

  &__before {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__icon {
    fill: currentColor;
  }

  &:hover {
    opacity: 0.7;
  }

  &--disabled {
    color: $grey-light-dark-color;
    background: $disabled-color;
    pointer-events: none;
  }

  &--outline {
    color: $main-color;
    background: transparent;
    border: 1px solid $main-color;

    &:hover {
      background: $main-color;
      color: $contrast-color;
    }
  }

  &--small {
    display: inline;
    padding: $button-small-padding;

    .bas-button__icon {
      width: 1em;
      height: 1em;
    }
  }

  &--rounded {
    width: 1.5em;
    height: 1.5em;
    padding: 0;
    border-radius: $border-radius-rounded;

    .bas-button__icon {
      width: 1em;
      height: 1em;
    }
  }
}
</style>
