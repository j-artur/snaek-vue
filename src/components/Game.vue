<template>
  <div class="game" @keydown="changeDirection($event)">
    <Button v-if="!running" @click="start" text="Play" />
    <Grid v-if="running" :grid="grid" />
  </div>
</template>

<script>
import Button from "./Button.vue";
import Grid from "./Grid.vue";

const createGrid = (size) => {
  let grid = [];

  for (let i = 0; i < size; i++) {
    const y = i;
    let line = [];
    for (let j = 0; j < size; j++) {
      const x = j;
      line = [...line, { player: false, food: false, coords: [x, y] }];
    }
    grid = [...grid, line];
  }

  return grid;
};

let loop;

export default {
  name: "Game",
  components: {
    Button,
    Grid,
  },
  props: {
    size: Number,
  },
  data() {
    return {
      running: false,
      player: {
        direction: null,
        pos: [],
      },
      food: [],
      plainGrid: [],
      speed: 5,
    };
  },
  computed: {
    grid() {
      return this.plainGrid.map((line, y) =>
        line.map((block, x) => ({
          ...block,
          player: !!this.player.pos.filter(
            (coords) => x == coords[0] && y == coords[1]
          ).length,
          food: x == this.food[0] && y == this.food[1],
          coords: [x, y],
        }))
      );
    },
  },
  methods: {
    start() {
      this.player.pos = [
        [3, Math.floor(this.size / 2)],
        [2, Math.floor(this.size / 2)],
        [1, Math.floor(this.size / 2)],
      ];

      this.food = [this.size - 3, Math.floor(this.size / 2)];

      this.running = true;

      loop = setInterval(this.move, (1 / this.speed) * 1000);
    },
    end() {
      this.running = false;

      this.player = {
        direction: null,
        pos: [],
      };

      this.food = [];

      clearInterval(loop);
    },
    move() {
      let [[x, y]] = this.player.pos;
      const size = this.size;
      switch (this.player.direction) {
        case "left":
          x = (--x + size) % size;
          break;
        case "up":
          y = (--y + size) % size;
          break;
        case "right":
          x = ++x % size;
          break;
        case "down":
          y = ++y % size;
          break;
        default:
          return;
      }
      this.player.pos = [[x, y], ...this.player.pos];
      this.player.pos.pop();
      if (x === this.food[0] && y === this.food[1]) this.eat();
      if (
        this.player.pos.filter((coords, i) => {
          if (i === 0) return false;
          else return x === coords[0] && y === coords[1];
        }).length
      )
        this.end();
    },
    eat() {
      const coords = this.player.pos;
      this.player.pos = [...coords, coords[coords.length - 1]];

      const newFood = [
        Math.floor(Math.random() * this.size),
        Math.floor(Math.random() * this.size),
      ];

      if (
        this.player.pos.filter(
          (coords) => newFood[0] === coords[0] && newFood[1] === coords[1]
        ).length
      )
        return this.eat();
      else this.food = newFood;
    },
    changeDirection(direction) {
      this.player.direction = direction;
    },
    handleKey({ key }) {
      if (
        (key === "ArrowLeft" || key === "a") &&
        this.player.direction !== "right" &&
        this.player.direction !== null
      )
        return this.changeDirection("left");
      if (
        (key === "ArrowUp" || key === "w") &&
        this.player.direction !== "down"
      )
        return this.changeDirection("up");
      if (
        (key === "ArrowRight" || key === "d") &&
        this.player.direction !== "left"
      )
        return this.changeDirection("right");
      if (
        (key === "ArrowDown" || key === "s") &&
        this.player.direction !== "up"
      )
        return this.changeDirection("down");
    },
  },
  mounted() {
    this.plainGrid = createGrid(this.size);

    window.addEventListener("keydown", this.handleKey);
  },
  unmounted() {
    window.removeEventListener("keydown", this.handleKey);
  },
};
</script>

<style lang="scss" scoped>
.game {
  max-width: 100vw;

  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
