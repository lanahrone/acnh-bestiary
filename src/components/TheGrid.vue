<template>
    <table border="1">
        <tr v-for="(r, rIndex) in Array(grid.height)" :key="`row${rIndex}`">
            <td v-for="(c, cIndex) in Array(grid.width)" :key="`cell${cIndex}`">
                {{ items[rIndex][cIndex] }}
            </td>
        </tr>
    </table>
</template>

<script>
export default {
    name: "TheGrid",
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
