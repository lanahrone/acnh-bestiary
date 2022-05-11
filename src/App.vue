<template>
  <div style="margin: 0 2rem;">
    <div>
      <button v-for="[gridType, grid] in Object.entries(grids)" :key="gridType" @click="currentGrid = grid">
        {{ grid.label }}
      </button>
    </div>

    <TheGrid v-if="currentGrid" :grid="currentGrid"></TheGrid>
  </div>
</template>

<script>
import insects from "./data/insects.json"
import fishes from "./data/fishes.json"
import TheGrid from "./components/TheGrid.vue"

export default {
  name: "App",
  components: { TheGrid },
  data() {
    return {
      currentGrid: null,
      grids: {
        insects: { type: "insects", width: 16, height: 5, label: "🦋", data: insects },
        fishes: { type: "fishes", width: 16, height: 5, label: "🐟", data: fishes },
        deepsea: { type: "deepsea", width: 8, height: 5, label: "🐚", data: [] },
      }
    }
  },
  mounted() {
    this.currentGrid = this.grids.insects
  }
}
</script>

<style>
body, html {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  background-color: #F8ECC3;
}
#app {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>
