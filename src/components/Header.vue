<template>
  <div class="header">
    <h1>{{ title }}</h1>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {
    title: String,
  },
};
</script>

<style lang="scss" scoped>
.header {
  padding: 1.5rem;

  background-color: #282c3433;
  box-shadow: 0 -0.5rem 1.5rem #0006;
}
</style>
