<template>
    <div class="keyboard">
        <div class="keyboardRow" v-for="(row, ind) in keys" :key="ind">
            <button
                v-for="(letter, ind) in row"
                :key="ind"
                @click="onButtonClick(letter)"
                :class="usedKeys.find((x) => x == letter) ? 'gray' : ''"
            >
                {{ letter }}
            </button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            keys: [
                ["q", "w", "e", "r", "t", "y", "u", "i", "o", "p"],
                ["a", "s", "d", "f", "g", "h", "j", "k", "l"],
                ["enter", "z", "x", "c", "v", "b", "n", "m", "del"],
            ],
            usedKeys: [],
        };
    },
    emits: ["click"],
    props: ["enabled", "validKeys"],
    methods: {
        onButtonClick(letter) {
            if (letter === "del" || letter === "enter") {
                this.$emit("click", letter);
                if (letter === "del") {
                    this.usedKeys.pop();
                }
            } else if (
                !this.usedKeys.find((x) => x == letter) &&
                this.enabled
            ) {
                this.usedKeys.push(letter);
                this.$emit("click", letter);
            }
        },
    },
};
</script>

<style scoped>
.keyboard {
    align-self: flex-end;
    flex-grow: 1;
    height: 28vh;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
    padding: 1rem;
}

.keyboardRow {
    display: flex;
    width: 100%;
    justify-content: center;
    gap: 1rem;
}

button {
    border: none;
    min-width: 3.3rem;
    height: 4rem;
    background-color: #fff;
    border-radius: 5px;
    box-shadow: rgba(78, 81, 85, 0.2) 0px 12px 24px;
    cursor: pointer;
    transition: all 0.1s ease-out;
    font-size: large;
    padding: 0.8em;
}

button:hover {
    transform: translateY(-12%);
}

button:active {
    transform: translateY(-3%);
}

.gray {
    background-color: #ddd;
}

.gray:hover {
    transform: none;
}
</style>
