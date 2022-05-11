<template>
  <button v-for="[gridType, grid] in Object.entries(grids)" :key="gridType" @click="currentGrid = grid">
    {{ grid.label }}
  </button>

  <TheGrid v-if="currentGrid" :grid="currentGrid"></TheGrid>
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
        insects: { width: 16, height: 5, label: "🦋", data: insects },
        fishes: { width: 16, height: 5, label: "🐟", data: fishes },
        deepsea: { width: 8, height: 5, label: "🐚", data: [] },
      }
    }
  }
}
</script>
