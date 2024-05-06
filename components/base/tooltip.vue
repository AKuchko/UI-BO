<template>
  <div class="base-tooltip">
    <transition name="fade">
      <div
        v-if="active"
        class="base-tooltip__content"
      >
        <slot name="tooltip" />
      </div>
    </transition>
    <div
      class="base-tooltip__trigger"
      @mouseover="setActive(true)"
      @mouseleave="setActive(false)"
    >
      <slot name="trigger" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'base-tooltip',
  props: {
    small: { type: Boolean, default: false },
    position: { type: String, default: 'auto' },
  },
  data () {
    return {
      active: false,
    };
  },
  computed: {
    classes () {
      return {
        'base-tooltip--active': this.active,
        'base-tooltip--small': this.small,
      };
    },
  },
  methods: {
    setActive (value) {
      this.active = value;
    },
  },
};
</script>

<style lang="scss">
.base-tooltip {
  position: relative;
  color: $contrast-color;

  &__content {
    position: absolute;
    top: 0;
    left: 50%;
    width: max-content;
    transform: translate(-50%, calc(-100% - 12px));
    padding: 12px 10px;
    border-radius: 5px;
    background: $grey-color;
  }

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s ease;
  }

  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
  }
}
</style>
