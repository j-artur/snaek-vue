<template>
  <div class="grid">
    <Line v-for="(line, idx) in grid" :line="line" :key="idx" />
  </div>
</template>

<script>
import Line from "./Line.vue";

export default {
  name: "Grid",
  components: {
    Line,
  },
  props: {
    grid: Array,
  },
};
</script>

<style>
.grid {
  padding: 1px;
  gap: 1px;

  width: 60vh;
  height: 60vh;

  background-color: #012;

  display: flex;
  flex-direction: column;
}
</style>
