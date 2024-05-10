<template>
  <transition name="fade" mode="out-in">
    <slot />
  </transition>
</template>

<script>
export default {
  name: 'transition-fade',
};
</script>

<style lang="scss">
.fade-enter-active,
.fade-leave-active {
  transition: all 0.25s ease;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
  scale: 0.95;
}
</style>
