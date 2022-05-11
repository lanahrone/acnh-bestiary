<template>
    <div class="cell"  @click="toggleOwnership()">
        <div v-if="availableThisMonth" :class="{ blink: isLastHour }" class="icon">{{ icon }}</div>
        <img :src="img" :alt="item.name" :style="{ opacity: availableNow ? 1 : 0.25 }" />
        <div v-if="owned" class="owned">✔️</div>
    </div>
</template>

<script>
export default {
    name: "TheCell",
    props: { item: Object, type: String },
    data() {
        const key = { 'insects': 'I', 'fishes': 'F', 'deepsea': 'D', }[this.type]
        return {
            img: require(`@/assets/img/${key}${this.item.id}.png`),
            ownedValue: null
        }
    },
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
        localStorageKey() {
            return `${this.type}_${this.item.id}`
        },
        owned: {
            get() {
                return !!this.ownedValue
            },
            set(newValue) {
                this.ownedValue = newValue
                window.localStorage.setItem(this.localStorageKey, newValue)
            }
        },
        icon() {
            if (this.isFirstMonth) return "🔵"
            else if (this.isLastMonth) return "🟠"
            else return "⚪"
        }
    },
    methods: {
        getSavedOwnership() {
            return parseInt(window.localStorage.getItem(this.localStorageKey) || 0)
        },
        toggleOwnership() {
            this.owned = this.getSavedOwnership() == 0 ? 1 : 0
        }
    }
}
</script>

<style>
    .cell {
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        width: 15vh;
        min-width: 100px;
        height: 15vh;
        min-height: 100px;
    }
    .cell img {
        width: 80%;
        max-width: 128px;
        height: 80%;
        max-height: 128px;
    }
    .icon {
        position: absolute;
        top: .25rem;
        right: .25rem;
    }
    .owned {
        position: absolute;
        bottom: .25rem;
        left: .25rem;
    }
    .blink {
        animation: blink-animation 1s infinite;
    }
    @keyframes blink-animation {
        0% { opacity: 1; }
        50% { opacity: .25; }
        100% { opacity: 1; }
    }
</style>
