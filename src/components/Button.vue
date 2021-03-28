<template>
  <button class="button" @click="onClick()" :style="{ background: color }">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    color: String,
    click: Function,
  },
  methods: {
    onClick() {},
  },
};
</script>

<style lang="scss" scoped>
.button {
  cursor: pointer;

  margin: 1rem;
  padding: 0.75rem 1.5rem;
  border: 1px solid #345;
  border-radius: 0.5rem;

  background-color: transparent;
  color: #fff;

  transition: all 0.15s ease-in-out;

  &:hover {
    background-color: #3456;
    border-color: transparent;
  }

  &:focus {
    outline: 0;
    background-color: #345f;
  }
}
</style>
