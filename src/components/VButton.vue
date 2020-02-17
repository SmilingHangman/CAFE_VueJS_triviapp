<template>
  <button
    :class="classList"
    @click="onClick"
  >
    <slot />
  </button>
</template>

<script>
export default {
  name: 'VButton',
  props: {
    primary: {
      type: Boolean,
      default: false
    },
    outlined: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    classList () {
      return [
        'primaryStyle',
        { outlinedStyle: this.outlined }
      ]
    }
  },
  methods: {
    onClick (event) {
      if (!this.disabled) {
        this.$emit('click', event)
      }
    }
  }
}
</script>

<style>
  .primaryStyle,
  .outlinedStyle {
    width: 305px;
    justify-self: flex-end;
    background-color: #fff;
    border: 1px solid #fff;
    border-radius: 20px;
    padding: 12px 0;
    font-family: fantasy;
    font-size: 16px;
    font-weight: 600;
    letter-spacing: 0.8px;
    color: rgb(45, 12, 66);
  }

  .outlinedStyle {
    border: 1px solid rgba(161, 88, 88);
  }

  .primaryStyle:hover,
  .outlinedStyle:hover {
    cursor: pointer;
  }

  .outlinedStyle:hover {
    color: #fff;
    background-color: rgb(50, 132, 187);
  }

</style>
