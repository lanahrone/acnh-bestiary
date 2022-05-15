<template>
  <div style="margin: 0 2rem;">
    <div>
      <button v-for="[gridType, grid] in Object.entries(grids)" :key="gridType" @click="changeGrid(grid)">
        {{ grid.label }}
      </button>

      <button style="margin-left: 2rem" @click="toggleMissing">💡</button>
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
  },
  methods: {
    changeGrid(newGrid) {
      this.currentGrid = null
      setTimeout(() => {
        this.currentGrid = newGrid
      }, 0);
    },
    toggleMissing() {
      window.dispatchEvent(new Event("highlight-missing"))
    }
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
button {
  min-width: 3rem;
  min-height: 3rem;
  margin: 0.25rem;
  background-color: #F8ECC3;
  border: 2px solid #E5DAB0;
  border-radius: 0.25rem;
  font-size: 1.25rem;
}
button:hover, button:active {
  background-color: #b8955344;
} 
button:first-of-type {
  margin-left: 0;
}
button:last-of-type {
  margin-right: 0;
}
</style>
