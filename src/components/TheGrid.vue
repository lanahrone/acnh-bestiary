<template>
    <table border="1">
        <tr v-for="(r, rIndex) in Array(grid.height)" :key="`row${rIndex}`">
            <td v-for="(c, cIndex) in Array(grid.width)" :key="`cell${cIndex}`">
                <TheCell :item="items[rIndex][cIndex]"></TheCell>
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
        }
    }
}
</script>
