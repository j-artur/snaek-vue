<template>
  <div :class="[player ? 'player' : '', food ? 'food' : '', 'block']"></div>
</template>

<script>
export default {
  name: "Block",
  props: {
    coords: Array,
    player: Boolean,
    food: Boolean,
  },
};
</script>

<style lang="scss" scoped>
.block {
  flex: 1 1 100%;

  background-color: #030609;
}
.food {
  background-color: #eba;
}
.player {
  background-color: #9be;
}
</style>
