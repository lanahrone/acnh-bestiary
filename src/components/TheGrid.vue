<template>
    <table cellspacing="0">
        <tr v-for="(r, rIndex) in Array(grid.height)" :key="`row${rIndex}`">
            <td v-for="(c, cIndex) in Array(grid.width)" :key="`cell${cIndex}`">
                <TheCell :type="this.grid.type" :item="items[rIndex][cIndex]"></TheCell>
            </td>
        </tr>
    </table>
</template>

<script>
import TheCell from "@/components/TheCell.vue"

export default {
    name: "TheGrid",
    components: { TheCell },
    props: { grid: Object },
    computed: {
        items() {
            const items = {}
            ;[...this.grid.data].forEach((item) => {
                const x = item.coords[0] - 1
                const y = item.coords[1] - 1
                if (items[x]) {
                    items[x][y] = item
                } else {
                    items[x] = { [y]: item }
                }
            })
            return items
        },
        savedData() {
            return window.localStorage[this.grid.type]
        }
    },
    created() {
        this.initLocalStorage(this.grid)
    },
    watch: {
        grid(newGrid) {
            this.initLocalStorage(newGrid)
        }
    },
    methods: {
        initLocalStorage(grid) {
            grid.data.forEach((item) => {
                const key = `${grid.type}_${item.id}`
                if (window.localStorage[key] === null || window.localStorage[key] === undefined) {
                    window.localStorage.setItem(key, 0)
                }
            })
        }
    }
}
</script>

<style scoped>
table {
    border: 1px solid #E5DAB0;
}
td {
    border: 1px solid #E5DAB0;
}
</style>
