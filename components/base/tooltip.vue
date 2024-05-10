<template>
  <div
    class="base-tooltip"
    :class="classes"
  >
    <transition-fade>
      <div
        v-if="active"
        ref="tooltip"
        class="base-tooltip__tooltip-content"
      >
        <slot name="tooltip" />
      </div>
    </transition-fade>
    <div
      ref="trigger"
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
    align: { type: String, default: 'auto' },
  },
  data () {
    return {
      active: false,
      class: 'base-tooltip',
    };
  },
  computed: {
    classes () {
      return {
        'base-tooltip--active': this.active,
        'base-tooltip--small': this.small,
        ...this.getPositionClasses(),
      };
    },
    canGetAutoClasses () {
      return typeof window !== 'undefined' &&
        typeof this.$refs.trigger !== 'undefined';
    }
  },
  methods: {
    setActive (value) {
      this.active = value;
    },
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
        typeof this.$refs.trigger === 'undefined'
      ) return {};


      const triggerRect = this.$refs.trigger.getBoundingClientRect();
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
        typeof this.$refs.trigger === 'undefined'
      ) return {};

      const triggerRect = this.$refs.trigger.getBoundingClientRect();
      const windowWidth = window.innerWidth;

      const alignRight = triggerRect.x + triggerRect.width > windowWidth - 100;
      const alignLeft = triggerRect.x < 100;
      const alignCenter = !alignRight && !alignLeft;

      return {
        [`${this.class}--left`]: alignLeft,
        [`${this.class}--right`]: alignRight,
        [`${this.class}--center`]: alignCenter,
      }
    },
  },
};
</script>

<style lang="scss">
.base-tooltip {
  position: relative;
  color: $tooltip-color;

  &__tooltip-content {
    position: absolute;
    width: max-content;
    padding: 12px 10px;
    border-radius: 5px;
    background: $grey-color;
    box-shadow: $tooltip-shadow;
    z-index: $z-middle;
    pointer-events: none;

    &::before {
      content: '';
      position: absolute;
      width: 1em;
      height: 1em;
      background: inherit;
    }
  }

  &--top {
    .base-tooltip__tooltip-content {
      top: 0;
      transform: translateY(calc(-100% - 12px));

      &::before {
        bottom: 0;
      }
    }
  }

  &--bottom {
    .base-tooltip__tooltip-content {
      bottom: 0;
      transform: translateY(calc(100% + 12px));

      &::before {
        top: 0;
      }
    }

    &:has(.base-tooltip--right) {
      .base-tooltip__tooltip-content::before {
        right: 10px;
        transform: rotate(45deg) translate(-50%, -50%);
      }
    }
  }

  &--center {
    .base-tooltip__tooltip-content {
      left: 50%;
    }

    .base-tooltip__tooltip-content::before {
      left: 50%;
    }

    &.base-tooltip--bottom {
      .base-tooltip__tooltip-content {
        transform: translate(-50%, calc(100% + 12px));
      }

      .base-tooltip__tooltip-content::before {
        transform: translate(-50%, -50%) rotate(45deg);
      }
    }

    &.base-tooltip--top {
      .base-tooltip__tooltip-content {
        transform: translate(-50%, calc(-100% - 12px));
      }

      .base-tooltip__tooltip-content::before {
        transform: translate(-50%, 50%) rotate(45deg);
      }
    }
  }

  &--left {
    .base-tooltip__tooltip-content {
      left: 0;
    }

    .base-tooltip__tooltip-content::before {
      left: 10px;
    }

    &.base-tooltip--bottom {
      .base-tooltip__tooltip-content::before {
        transform: translateY(-50%) rotate(45deg);
      }
    }

    &.base-tooltip--top {
      .base-tooltip__tooltip-content::before {
        transform: translateY(50%) rotate(45deg);
      }
    }
  }

  &--right {
    .base-tooltip__tooltip-content {
      right: 0;
    }

    .base-tooltip__tooltip-content::before {
      right: 10px;
    }

    &.base-tooltip--bottom {
      .base-tooltip__tooltip-content::before {
        transform: translateY(-50%) rotate(45deg);
      }
    }

    &.base-tooltip--top {
      .base-tooltip__tooltip-content::before {
        transform: translateY(50%) rotate(45deg);
      }
    }
  }
}
</style>
