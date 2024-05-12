<template>
  <div class="user-item">
    <user-avatar
      :name="name",
      :current-user="isCurrentUser"
    />
    <p class="user-item__name">{{ name }}</p>
    <p class="user-item__status">{{ status }}</p>
  </div>
</template>

<script>
export default {
  name: 'user-item',
  props: {
    name: { type: String, required: true },
    status: { type: String, default: '' },
    isCurrentUser: { type: Boolean, default: false },
  },
};
</script>

<style lang="scss">
.user-item {
  display: flex;
  align-items: center;
  gap: 5px;
}
</style>
