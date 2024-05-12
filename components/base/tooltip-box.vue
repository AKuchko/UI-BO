<template>
  <div
    class="base-tooltip-box"
    :class="classes"
  >
    <slot />
  </div>
</template>

<script>
export default {
  name: 'base-tooltip-box',
  props: {
    position: { type: String, default: 'auto' },
    align: { type: String, default: 'auto' },
  },
  data () {
    return {
      class: 'base-tooltip-box',
    };
  },
  computed: {
    classes () {
      return this.getPositionClasses();
    },
  },
  methods: {
    getPositionClasses () {
      return {
        ...(
          this.position === 'auto'
            ? this.getAutoPositionClasses()
            : { [`${this.class}--${this.position}`]: true }
        ),
        ...(
          this.align === 'auto'
            ? this.getAutoAlignClasses()
            : { [`${this.class}--${this.align}`]: true }
        ),
      };
    },
    getAutoPositionClasses () {
      if (
        typeof window === 'undefined' ||
        typeof this.$parent === 'undefined'
      ) return {};

      const parent = this.$parent.$el.parentElement;

      if (!parent) return {};

      const triggerRect = parent.getBoundingClientRect();
      const windowHeight = window.innerHeight;

      const positionBottom = triggerRect.y < 50;
      const positionTop = !positionBottom || triggerRect.y > windowHeight - 50;

      return {
        [`${this.class}--bottom`]: positionBottom,
        [`${this.class}--top`]: positionTop,
      };
    },
    getAutoAlignClasses () {
      if (
        typeof window === 'undefined' ||
        typeof this.$parent === 'undefined'
      ) return {};

      const parent = this.$parent.$el.parentElement;

      if (!parent) return {};

      const triggerRect = parent.getBoundingClientRect();
      const windowWidth = window.innerWidth;

      const alignRight = triggerRect.x + triggerRect.width > windowWidth - 100;
      const alignLeft = triggerRect.x < 100;
      const alignCenter = !alignRight && !alignLeft;

      return {
        [`${this.class}--left`]: alignLeft,
        [`${this.class}--right`]: alignRight,
        [`${this.class}--center`]: alignCenter,
      };
    },
    getYOverflow () {

    }
  }
}
</script>

<style lang="scss">
.base-tooltip-box {
  position: absolute;

  width: max-content;

  border-radius: 5px;
  background: $grey-color;
  box-shadow: $tooltip-shadow;

  z-index: $z-middle;

  &::before {
    content: '';
    position: absolute;
    width: 1em;
    height: 1em;
    background: inherit;
    z-index: $z-negative;
  }

  &--top {
    top: 0;
    transform: translateY(calc(-100% - 12px));

    &::before {
      bottom: 0;
    }
  }

  &--bottom {
    bottom: 0;
    transform: translateY(calc(-100% - 12px));

    &::before {
      top: 0;
    }
  }

  &--left {
    left: 0;

    &::before {
      left: 10px;
    }

    &.base-tooltip-box--bottom {
      &::before {
        transform: translateY(-50%) rotate(45deg);
      }
    }

    &.base-tooltip-box--top {
      &::before {
        transform: translateY(50%) rotate(45deg);
      }
    }
  }

  &--right {
    right: 0;

    &::before {
      right: 10px;
    }

    &.base-tooltip-box--bottom {
      &:before {
        transform: translateY(-50%) rotate(45deg);
      }
    }

    &.base-tooltip-box--top {
      &::before {
        transform: translateY(50%) rotate(45deg);
      }
    }
  }

  &--center {
    left: 50%;

    &:before {
      left: 50%;
    }

    &.base-tooltip-box--bottom {
      transform: translate(-50%, calc(100% + 12px));

      &::before {
        transform: translate(-50%, -50%) rotate(45deg);
      }
    }

    &.base-tooltip-box--top {
      transform: translate(-50%, calc(-100% - 12px));

      &::before {
        transform: translate(-50%, 50%) rotate(45deg);
      }
    }
  }
}
</style>
