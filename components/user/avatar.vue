<template>
  <div
    class="user-avatar"
    :class="classes"
    :style="styles"
  >
    <span>
      {{ name[0] }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'user-avatar',
  props: {
    currentUser: { type: Boolean, default: false },
    name: { type: String, required: true },
  },
  computed: {
    classes () {
      return {
        'user-avatar--current-user': this.currentUser,
      };
    },
    styles () {
      return {
        background: this.stringToColour(this.name),
      };
    },
  },
  methods: {
    stringToColour (str) {
      let hash = 0;
      str.split('').forEach(char => {
        hash = char.charCodeAt(0) + ((hash << 5) - hash)
      });
      console.log(hash);
      let colour = '#';
      for (let i = 0; i < 3; i++) {
        const value = (hash >> (i * 4)) & 0xff;
        colour += value.toString(16).padStart(2, '0');
        console.log(value, colour);
      }
      console.log(colour);
      return colour

      // let hash = 0;
      // for (let i = 0; i < str.length; i++) {
      //   hash = str.charCodeAt(i) + ((hash << 5) - hash);
      // }
      // console.log(hash);
      // const c = (hash & 0x00FFFFFF)
      //   .toString(16)
      //   .toUpperCase();

      // console.log(c, '#' + "00000".substring(0, 6 - c.length) + c);

      // return '#' + "00000".substring(0, 6 - c.length) + c;
    }
  }
};
</script>

<style lang="scss" scoped>
  .user-avatar {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: $border-radius-rounded;
    width: 20px;
    height: 20px;

    font-size: 14px;
    text-align: center;
    line-height: 20px;
    letter-spacing: 0;
    color: $contrast-color;

    &--current-user {
      &::after {
        content: '';
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 18px;
        height: 18px;
        border: 1px solid $contrast-color;
        border-radius: $border-radius-rounded;
      }
    }
  }
</style>
