<template>
  <Header title="Snaek is Frend" />
  <Game :size="15" />
</template>

<script>
import Header from "./components/Header.vue";
import Game from "./components/Game.vue";

export default {
  name: "App",
  components: {
    Header,
    Game,
  },
};
</script>

<style lang="scss">
*,
*::before,
*::after {
  margin: 0;
  padding: 0;

  font-family: "Ubuntu", "Open Sans", Helvetica, Arial, sans-serif;

  box-sizing: border-box;
}

body {
  background-color: #20252b;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

  color: #fff;
}
</style>
