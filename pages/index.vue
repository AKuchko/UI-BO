<template>
  <div class="main">
    <div class="buttons">
      <base-button title="Button" />
      <base-button title="Button" disabled />
      <base-button title="Button" outlined />
      <base-button title="Button" icon="icon-cog" @click="addP" />
    </div>
    <div class="buttons-small">
      <base-button title="Button" small />
      <base-button small icon="icon-cog" />
      <base-button small icon="icon-cog" outlined />
      <base-button rounded icon="icon-cog" />
    </div>
    <div class="buttons-small">
      <base-text-field label="Text field" />
    </div>
    <div class="buttons-small">
      <base-chip>
        Base chip
      </base-chip>
      <base-chip accent>
        Base chip
      </base-chip>
    </div>
    <div class="buttons">
      <p v-for="p in ps">{{ p }}</p>
      <base-tooltip>
        <template v-slot:trigger>
          <base-chip accent>
            Base chip
          </base-chip>
        </template>
        <template v-slot:tooltip>
          Tooltip content text
        </template>
      </base-tooltip>
      <base-tooltip>
        <template v-slot:trigger>
          <base-chip accent>
            Base chip
          </base-chip>
        </template>
        <template v-slot:tooltip>
          Tooltip content text
        </template>
      </base-tooltip>
      <base-tooltip>
        <template v-slot:trigger>
          <base-chip accent>
            Base chip
          </base-chip>
        </template>
        <template v-slot:tooltip>
          Tooltip content text
        </template>
      </base-tooltip>
      <base-dots-menu />
      <p v-for="p in ps">{{ p }}</p>
    </div>
    <div class="buttons">
      <base-dots-menu />
      <user-avatar name="Кучко Алексанндр Сергеевич" />
      <user-avatar name="Стул 120" />
      <user-avatar name="Михаил Грунев" />
      <user-avatar name="Скултан Юлия" current-user />
      <user-avatar name="Елисеев Владислав Сергеевич" current-user />
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
      ps: [],
    };
  },
  methods: {
    addP () {
      this.ps.push('p')
    }
  }
}
</script>

<style lang="scss">
.main {
  padding: 20px;
  display: flex;
  gap: 20px;
  flex-wrap: wrap;

  .buttons {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .buttons-small {
    display: flex;
    align-items: flex-start;
    gap: 10px;
  }
}
</style>
