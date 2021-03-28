<template>
  <div class="line">
    <Block
      v-for="(block, idx) in line"
      :coords="block.coords"
      :player="block.player"
      :food="block.food"
      :key="idx"
    />
  </div>
</template>

<script>
import Block from "./Block.vue";

export default {
  name: "Line",
  components: {
    Block,
  },
  props: {
    line: Array,
  },
};
</script>

<style lang="scss" scoped>
.line {
  gap: 1px;

  flex: 1 1 100%;

  display: flex;
  flex-direction: row;
}
</style>
