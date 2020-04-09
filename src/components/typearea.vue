<template>
    <div class="area my-auto flex flex-col justify-center items-center">
        <span
            class="text-center redo-trigger bg-blue-800 text-white font-semibold border border-blue-500 rounded text-xl mb-2"
            >{{ timeCount }}</span>
        <div class="main-type bg-teal-200 p-4 rounded-lg ">
            <div
                class="text-display mb-4 text-blue-800 text-xl md:text-2xl font-semibold bg-teal-100 textdisplay"
                ref="display">
                <span :class="{ 'highlight' : key == currentWord }" v-for="(word, key) in wordList" :key="key">
                    {{ word }}
                </span>
            </div>
            <div class="flex justify-between">
                <input
                    v-bind:class="{ error : hasWrong }"
                    v-model="inputWord"
                    @keydown="keyin('input', $event)"
                    type="text"
                    name=""
                    id=""
                    ref="inputField"
                    class="textarea p-3 bg-teal-600 text-white rounded-lg border-teal-600 outline-none focus:border-teal-400 border-8 text-xl md:text-2xl"
                />
                <button
                    class="redo-trigger bg-blue-800 hover:bg-blue-500 text-white font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded text-xl"
                    @click="textRender"
                >
                    Redo
                </button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "typearea",
    props: {
        randomWords: Object,
    },

    data() {
        return {
            wordList: [],
            currentWord: 0,
            correctKeys: 0,
            inputWord: "",
            hasWrong: false,
            timeCount: 60,
            timer: 0,
            timerActive: false,
        };
    },

    methods: {
        textRender() {
            this.wordList = [];
            this.timeCount = 60;
            this.currentWord = 0;
            this.correctKeys = 0;
            this.timerActive = false;
            clearTimeout(this.timer);
            for (let i = 0; i < 100; i++) {
                let n = Math.floor(
                    Math.random() * this.randomWords.english.length
                );
                this.wordList.push(this.randomWords.english[n]);
            }
            this.$refs.inputField.focus();
            this.$refs.inputField.value = "";
            this.inputWord = "";
            // this.$refs.display.firstChild.classList.add("highlight");
        },

        keyin(where, e) {
            let inputField = this.$refs.inputField;
            let textDisplay = this.$refs.display;
            if (this.timerActive) this.inputField(e);

            if (this.currentWord === 0 && inputField.value === "") {
                if (!this.timerActive) {
                    this.startTimer();
                    this.timerActive = true;
                }
            }

            if (e.key === ' ') {
                e.preventDefault();

                if (inputField.value !== '') {
                    const currentWordPosition = textDisplay.childNodes[this.currentWord].getBoundingClientRect();
                    const nextWordPosition = textDisplay.childNodes[this.currentWord + 1].getBoundingClientRect();
                    if (currentWordPosition.top < nextWordPosition.top) {
                        for (let i = 0; i < this.currentWord + 1; i++) {
                            textDisplay.childNodes[i].style.display = 'none';
                        }
                    }

                    if (this.currentWord < this.wordList.length - 1) {
                        if (inputField.value === this.wordList[this.currentWord]) {
                            textDisplay.childNodes[this.currentWord].classList.add('correct');
                            this.correctKeys += this.wordList[this.currentWord].length + 1;
                        } else {
                            textDisplay.childNodes[this.currentWord].classList.add('wrong');
                        }
                        textDisplay.childNodes[this.currentWord + 1].classList.add('highlight');
                    } else if (this.currentWord === this.wordList.length - 1) {
                        textDisplay.childNodes[this.currentWord].classList.add('wrong');
                        this.showResult();
                    }
                    inputField.value = '';
                    this.inputWord = "";
                    this.currentWord++;
                }
            } else if (this.currentWord === this.wordList.length - 1) {
                if (inputField.value + e.key === this.wordList[this.currentWord]) {
                    textDisplay.childNodes[this.currentWord].classList.add('correct');
                    this.correctKeys += this.wordList[this.currentWord].length;
                    this.currentWord++;
                    this.showResult();
                }
            }
        },

        inputField(e) {
            let inputField = this.$refs.inputField;
            if ((e.key >= "a" && e.key <= "z") || e.key === `'` || e.key === "," || e.key === "." || e.key === ";") {
                let inputWordSlice = inputField.value + e.key;
                let currentWordSlice = this.wordList[this.currentWord].slice( 0, inputWordSlice.length);
                inputWordSlice === currentWordSlice
                    ? console.log("same")
                    : console.log("wrong");
                inputWordSlice === currentWordSlice
                    ? (this.hasWrong = false)
                    : (this.hasWrong = true);
            } else if (e.key === "Backspace") {
                let inputWordSlice = e.ctrlKey
                    ? ""
                    : inputField.value.slice(0, inputField.value.length - 1);
                let currentWordSlice = this.wordList[this.currentWord].slice(0, inputWordSlice.length);
                inputWordSlice === currentWordSlice
                    ? (this.hasWrong = false)
                    : (this.hasWrong = true);
            } else if (e.key === " ") {
                this.hasWrong = false;
            }
            console.log(e.key);
        },

        startTimer() {
            let time = 60;
            if (this.timeCount > 0) {
                this.timer = time;
                this.timer = setTimeout(() =>{
                    this.timeCount--;
                    this.startTimer(time);
                }, 1000);
            } else {
                this.timerActive = false;
                this.timeCount = 60
                this.showResult();
            }
        },

        showResult() {
            this.textRender();
            alert("done done done");
        }
    },
    watch: {
        handleInput() {
            if (this.inputWord) {
                this.handler(this.timer);
            }
        },

        timerCount: {
            handler(timer) {
                if (timer > 0) {
                    setTimeout(() => {
                        this.timer--;
                    }, 1000);
                }
            },
            immediate: true, // This ensures the watcher is triggered upon creation
        },
    },
};
</script>

<style lang="scss" scoped>
.area {
    width: 100%;
    height: 70%;

    .main-type {
        width: 50%;
    }

    .textarea {
        width: 78%;
    }

    .redo-trigger {
        width: 20%;
    }

    .textdisplay {
        height: 5rem;
        padding: 8px;
        overflow: hidden;
    }

    .highlight {
        color: #dd6b20;
    }

    .error {
        background-color: #4299e1;
    }

    .wrong {
        color: red;
    }

    .correct {
        color: gray;
    }
}
</style>
