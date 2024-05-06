<template>
  <div
    class="base-chip"
    :class="classes"
  >
    <slot />
  </div>
</template>

<script>
export default {
  name: 'base-chip',
  props: {
    accent: { type: Boolean, default: false },
  },
  computed: {
    classes () {
      return {
        'base-chip--accent': this.accent,
      };
    },
  },
};
</script>

<style lang="scss">
.base-chip {
  border-radius: 16px;
  padding: 9.5px 12px;
  color: $black-color;
  background: #e0e0e0;

  &--accent {
    color: $main-color;
    background: $main-light-color;
  }
}
</style>
