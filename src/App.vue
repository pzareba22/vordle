<template>
    <div class="main">
        <header class="mainHeader">
            <h1>Vordle</h1>
            <p>By Paweł Zaręba</p>
        </header>
        <div class="letterGrid">
            <div class="letterRow" v-for="(row, ind) in letters" :key="ind">
                <LetterSquare
                    v-for="(letter, ind2) in row"
                    :key="ind2"
                    :letter="letter"
                    :class="colors[ind][ind2]"
                />
            </div>
        </div>
        <Keyboard
            @click="updateLetter"
            :enabled="currentCol < 5"
            :greenKeys="greenKeys"
            :yellowKeys="yellowKeys"
            :grayKeys="grayKeys"
            ref="keyboard"
        />
    </div>
</template>

<script>
/*
##TODO:
    - [x] Sprawdzenie czy submitowane słowo jest poprawne
    - [x] Sprawdzenie liter submitowanego słowa
    - [x] Przekazanie 'żółtych' i 'zielonych' liter
    - [ ] Komunikaty o wygranej i przegranej
    - [ ] Help
    - [ ] Optymalizacja szukania słów w wordliście
*/

import LetterSquare from "./components/LetterSquare.vue";
import Keyboard from "./components/Keyboard.vue";
import wordList from "./words";

export default {
    data() {
        return {
            letters: Array.from(Array(6), () => new Array(5).fill(" ")),
            colors: Array.from(Array(6), () => new Array(5).fill("")),
            currentRow: 0,
            currentCol: 0,
            greenKeys: [],
            yellowKeys: [],
            grayKeys: [],
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
            } else if (letter === "enter") {
                if (this.currentCol == 5) this.validateWord();
            } else {
                if (this.currentCol < 5) {
                    this.letters[this.currentRow][this.currentCol] = letter;
                    this.currentCol += 1;
                }
            }
        },
        validateWord() {
            let currWord = "";
            for (let i = 0; i < 5; i++) {
                if (this.letters[this.currentRow][i] === " ") {
                    return;
                }
                currWord += this.letters[this.currentRow][i];
            }

            // Enable checking if the word is in the dictionary

            // if (!wordList.find((x) => x === currWord)) {
            //     window.alert("Word is not on the wordlist :c");
            //     return;
            // }
            console.log(`Submitted word is: ${currWord}`);

            for (let i = 0; i < 5; i++) {
                if (currWord[i] === this.word[i]) {
                    this.colors[this.currentRow][i] = "green";
                    this.greenKeys.push(currWord[i]);
                } else if (this.word.search(currWord[i]) != -1) {
                    this.colors[this.currentRow][i] = "yellow";
                    this.yellowKeys.push(currWord[i]);
                } else {
                    this.colors[this.currentRow][i] = "gray";
                    this.grayKeys.push(currWord[i]);
                }
            }
            this.currentRow += 1;
            this.currentCol = 0;
            this.$refs.keyboard.clearKeys();
        },
    },
    created() {
        const ind = Math.floor(Math.random() * wordList.length);
        this.word = wordList[ind];
        console.log("Chosen word is: ");
        console.log(this.word);
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
    min-width: 55vw;
    height: 100vh;
    margin: 0 auto;
    background-color: #fdfdfd;
    display: flex;
    flex-direction: column;
    align-items: center;
    position: relative;
}

.mainHeader {
    background-color: #bfee9b;
    color: #fff;
    text-align: center;
    font-size: x-large;
    letter-spacing: 0.3rem;
    width: 100%;
    position: absolute;
    top: 0;
    bottom: 83vh;
    animation: full_out 2s ease-out;
    transition: all;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

.mainHeader p {
    font-size: medium;
    font-family: "Courier New", Courier, monospace;
}

.letterGrid {
    flex-grow: 8;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    margin-top: 17vh;
}

.letterRow {
    display: flex;
    gap: 0.5em;
}

@keyframes full_out {
    0% {
        top: 0;
        bottom: 0;
    }

    50% {
        top: 0;
        bottom: 0;
    }

    100% {
        top: 0;
        bottom: 83vh;
    }
}
</style>

<style>
.gray {
    background-color: #ddd !important;
}

.gray2 {
    background-color: rgb(128, 125, 125) !important;
}

.green {
    background-color: rgb(151, 252, 112) !important;
}

.yellow {
    background-color: rgb(250, 215, 102) !important;
}
</style>
