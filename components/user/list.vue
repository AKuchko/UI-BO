<template>
  <ul class="user-list">
    <base-toolip
      v-for="(user, index) in users"
      :key="index"
    >
      <template name="tooltip">
        <user-item
          :name="user.name"
          :is-current-user="isCurrentUser(user.id)"
        />
      </template>
      <template name="trigger">
        <user-avatar
          :name="user.name"
          :is-current-user="isCurrentUser(user.id)"
        />
      </template>
    </base-toolip>
  </ul>
</template>

<script>
export default {
  name: 'user-list',
  props: {
    users: { type: Array, default: () => [] },
    currentUser: { type: Object, default: () => ({}) },
  },
  methods: {
    isCurrentUser (userId) {
      if (
        !userId ||
        !this.currentUser ||
        !Object.keys(this.currentUser).length ||
        !this.currentUser.id
      ) return false;
      return this.currentUser.id === userId;
    }
  },
};
</script>
