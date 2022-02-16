<template>
    <div class="keyboard">
        <div class="keyboardRow" v-for="(row, ind) in keys" :key="ind">
            <button
                v-for="(letter, ind) in row"
                :key="ind"
                @click="onButtonClick(letter)"
                :class="keyClass(letter)"
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
    props: ["enabled", "yellowKeys", "greenKeys", "grayKeys"],
    methods: {
        onButtonClick(letter) {
            if (letter === "del" || letter === "enter") {
                this.$emit("click", letter);
                if (letter === "del") {
                    this.usedKeys.pop();
                }
            } else if (this.enabled) {
                this.usedKeys.push(letter);
                this.$emit("click", letter);
                console.log(this.usedKeys);
            }
        },
        keyClass(key) {
            let res = "";
            if (this.greenKeys.find((x) => x == key)) {
                res = "green";
            } else if (this.yellowKeys.find((x) => x == key)) {
                res = "yellow";
            } else if (this.grayKeys.find((x) => x == key)) {
                res = "gray2 noHover";
            } else if (this.usedKeys.find((x) => x == key)) {
                res = "gray";
            }
            return res;
        },
        clearKeys() {
            this.usedKeys = [];
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
    gap: 0.5rem;
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

.noHover {
    transform: none !important;
}
</style>
