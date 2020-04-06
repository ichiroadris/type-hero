<template>
    <div class="area my-auto flex flex-col justify-center items-center">
        <span class="text-center redo-trigger bg-blue-800 text-white font-semibold border border-blue-500 rounded text-xl mb-2" v-if="timer != 0">{{ timer }}</span>
        <div class="main-type bg-teal-200 p-4 rounded-lg ">
            <div class="text-display mb-4 text-blue-800 text-xl md:text-2xl font-semibold bg-teal-100 textdisplay" ref="display">
                <span v-for="(word, key) in wordList" :key="key"> {{ word }}</span>
            </div>
            <div class="flex justify-between">
                <input v-model="inputWord" @keyup="keyin('input', $event)" type="text" name="" id="" ref="inputField" class="textarea p-3 bg-teal-600 text-white rounded-lg border-teal-600 outline-none focus:border-teal-400 border-8 text-xl md:text-2xl">
                <button class="redo-trigger bg-blue-800 hover:bg-blue-500 text-white font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded text-xl" @click="textRender">Redo</button>
            </div>

        </div>
    </div>
</template>

<script>
    export default {
        name: "typearea",
        props: {
            randomWords: Object
        },

        data () {
            return {
                wordList: [],
                currentWord: 0,
                correctKeys: 0,
                timerActive: false,
                inputWord: '',
                timer: 60
            }
        },

        methods: {
            textRender() {
                this.wordList = [];
                this.currentWord = 0;
                this.correctKeys = 0;
                this.timerActive = false;
                clearTimeout(this.timer);
                for (let i = 0;i < 100; i++) {
                    let n = Math.floor(Math.random() * this.randomWords.english.length)
                    this.wordList.push(this.randomWords.english[n]);
                }
                this.$refs.inputField.focus();
                this.$refs.inputField.value = '';
                this.inputWord = "";
                this.$refs.display.firstChild.classList.add('highlight');
            },

            keyin(where, e) {
                if (!this.timerActive) this.inputField(e);
            },

            inputField(e) {
                if (e.key >= 'a' && e.key <= 'z' || (e.key === `'` || e.key === ',' || e.key === '.' || e.key === ';')) {
                    let inputWordSlice = this.$refs.inputField.value + e.key;
                    console.log(inputWordSlice);
                    // let currentWordSlice = this.wordList[this.currentWord].slice(0, inputWordSlice.length);
                    // this.$refs.inputField.className = inputWordSlice === currentWordSlice ? '' : 'wrong';
                }
                console.log(e.key);
            },

        },

            // showText() {
            //     wordList.forEach(word => {

            //     })
            // }
        watch: {

            handleInput() {
                if(this.inputWord) {
                    this.handler(this.timer)
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
                immediate: true // This ensures the watcher is triggered upon creation
            }

        }

    }
</script>

<style lang="scss" scoped>
    .area {
        width: 100%;
        height: 70%;

        .main-type {
            width: 50%
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
            overflow:hidden;
        }

        .highlight {
            color:  #dd6b20;
        }
    }

</style>