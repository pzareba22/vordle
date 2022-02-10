<template>
    <div class="main">
        <header class="mainHeader">
            <h1>Vordle</h1>
        </header>
        <div class="letterGrid">
            <div class="letterRow" v-for="(row, ind) in letters" :key="ind">
                <LetterSquare
                    v-for="(letter, ind2) in row"
                    :key="ind2"
                    :letter="letter"
                />
            </div>
        </div>
        <Keyboard
            @click="updateLetter"
            :enabled="currentCol < 6"
            :validKeys="validKeys"
        />
    </div>
</template>

<script>
import LetterSquare from "./components/LetterSquare.vue";
import Keyboard from "./components/Keyboard.vue";
export default {
    data() {
        return {
            letters: Array.from(Array(5), () => new Array(6).fill(" ")),
            currentRow: 0,
            currentCol: 0,
            validKeys: ["a"],
            word: "",
        };
    },
    components: {
        LetterSquare,
        Keyboard,
    },
    methods: {
        updateLetter(letter) {
            if (letter === "del") {
                if (this.currentCol > 0) {
                    this.letters[this.currentRow][this.currentCol - 1] = " ";
                    this.currentCol -= 1;
                }
            } else {
                if (this.currentCol < 6) {
                    this.letters[this.currentRow][this.currentCol] = letter;
                    this.currentCol += 1;
                }
            }
        },
    },
};
</script>

<style scoped>
* {
    font-family: sans-serif;
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

.main {
    width: 55vw;
    height: 100vh;
    margin: 0 auto;
    background-color: #fdfdfd;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.mainHeader {
    background-color: #bfee9b;
    color: #fff;
    padding: 2rem 0;
    text-align: center;
    font-size: x-large;
    letter-spacing: 0.3rem;
    width: 100%;
}

.letterGrid {
    flex-grow: 8;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1em;
}

.letterRow {
    display: flex;
    gap: 0.5em;
}
</style>
