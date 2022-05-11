<template>
    <div v-if="availableThisMonth" :class="{ blink: isLastHour }" :style="{ opacity: availableNow ? 1 : 0.25 }">{{ icon }}</div>
</template>

<script>
export default {
    name: "TheCell",
    props: { item: Object },
    computed: {
        currentMonth: () => new Date().getMonth() + 1,
        currentHour: () => new Date().getHours(),
        availableThisMonth() {
            return this.item.months_north.includes(this.currentMonth)
        },
        isFirstMonth() {
            return this.availableThisMonth && !this.item.months_north.includes(this.currentMonth - 1)
        },
        isLastMonth() {
            return this.availableThisMonth && !this.item.months_north.includes(this.currentMonth + 1)
        },
        availableNow() {
            return this.item.hours.includes(this.currentHour)
        },
        isLastHour() {
            return this.availableNow && !this.item.hours.includes(this.currentHour + 1)
        },
        icon() {
            if (this.isFirstMonth) return "🔵"
            else if (this.isLastMonth) return "🟠"
            else return "⚪"
        }
    }
}
</script>

<style>
    .blink {
        animation: blink-animation 1s infinite;
    }
    @keyframes blink-animation {
        0% { opacity: 1; }
        50% { opacity: .25; }
        100% { opacity: 1; }
    }
</style>
