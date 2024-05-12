<template>
  <div class="base-dots-menu">
    <button
      class="base-dots-menu__dots"
      @click="toggleActive"
    >
      <span class="base-dots-menu__dot" />
      <span class="base-dots-menu__dot" />
      <span class="base-dots-menu__dot" />
    </button>
    <transition-fade>
      <base-tooltip-box v-if="active">
        <ul class="base-dots-menu__menu">
          <button class="base-dots-menu__item">
            Action 1
          </button>
          <button class="base-dots-menu__item">
            Action 1
          </button>
          <button class="base-dots-menu__item">
            Action 1
          </button>
          <button class="base-dots-menu__item">
            Action 1
          </button>
        </ul>
      </base-tooltip-box>
    </transition-fade>
  </div>
</template>

<script>
export default {
  name: 'base-dots-menu',
  props: {
    menu: { type: Array, default: () => [] },
    position: { type: String, default: 'auto' },
    align: { type: String, default: 'auto' },
  },
  data () {
    return {
      active: false,
      class: 'base-dots-menu',
    };
  },
  // computed: {
  //   classes () {
  //     return {};
  //   },
  // },
  methods: {
    toggleActive () {
      this.active = !this.active;
    },
    setActive (value) {
      this.active = value;
    },
    // getPositionClasses () {
    //   return {
    //     ...(
    //       this.position === 'auto'
    //         ? this.getAutoPositionClasses()
    //         : { [`${this.class}--${this.position}`]: true }
    //     ),
    //     ...(
    //       this.align === 'auto'
    //         ? this.getAutoAlignClasses()
    //         : { [`${this.class}--${this.align}`]: true }
    //     ),
    //   };
    // },
    // getAutoPositionClasses () {
    //   if (
    //     typeof window === 'undefined' ||
    //     typeof this.$refs.trigger === 'undefined'
    //   ) return {};


    //   const triggerRect = this.$refs.trigger.getBoundingClientRect();
    //   const windowHeight = window.innerHeight;

    //   const positionBottom = triggerRect.y < 50;
    //   const positionTop = !positionBottom || triggerRect.y > windowHeight - 50;

    //   return {
    //     [`${this.class}--bottom`]: positionBottom,
    //     [`${this.class}--top`]: positionTop,
    //   };
    // },
    // getAutoAlignClasses () {
    //   if (
    //     typeof window === 'undefined' ||
    //     typeof this.$refs.trigger === 'undefined'
    //   ) return {};

    //   const triggerRect = this.$refs.trigger.getBoundingClientRect();
    //   const windowWidth = window.innerWidth;

    //   const alignLeft = triggerRect.x + triggerRect.width > windowWidth - 100;
    //   const alignRight = triggerRect.x < 100;
    //   const alignCenter = !alignRight && !alignLeft;

    //   return {
    //     [`${this.class}--left`]: alignLeft,
    //     [`${this.class}--right`]: alignRight,
    //     [`${this.class}--center`]: alignCenter,
    //   };
    // },
  }
};
</script>

<style lang="scss">
.base-dots-menu {
  display: inline-block;
  position: relative;

  width: min-content;

  &__dots {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 2px;
    width: 25px;
    height: 25px;

    &:hover {
      opacity: 0.7;
    }
  }

  &__dot {
    display: block;
    width: 4px;
    height: 4px;
    border-radius: $border-radius-rounded;
    background: $grey-color;
  }

  &__menu {
    display: flex;
    flex-direction: column;
    padding: 5px 0;
    color: $contrast-color;
  }

  &__item {
    padding: 8px 18px;
  }
}
</style>
