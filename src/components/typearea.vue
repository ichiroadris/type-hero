<template>
    <div class="area my-auto flex justify-center items-center">
        <div class="main-type bg-teal-200 p-8 rounded-lg">
            <div class="text-display mb-4 text-blue-800 text-xl md:text-2xl font-semibold bg-teal-100">
                <span v-for="word in wordList" :key="word"> {{ word }}</span>
            </div>
            <div class="flex justify-between">
                <input v-model="inputWord" type="text" name="" id="" class="textarea p-3 bg-teal-600 text-white rounded-lg border-teal-600 outline-none focus:border-teal-400 border-8 text-xl md:text-2xl">

                <button class="redo-trigger bg-blue-800 hover:bg-blue-500 text-white font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded text-xl" v-if="timer == 0">Redo</button>
                <span class="redo-trigger bg-blue-800 text-white font-semibold border border-blue-500 rounded text-xl" v-if="timer != 0">{{ timer }}</span>
            </div>
            <span class="redo-trigger bg-blue-800 text-white font-semibold border border-blue-500 rounded text-xl" v-if="timer != 0">{{ inputWord }}</span>
            <button @click.prevent="textRender" class="redo-trigger bg-blue-800 hover:bg-blue-500 text-white font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded text-xl">Redo</button>

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
                for (let i = 0;i < 100; i++) {
                    let n = Math.floor(Math.random() * this.randomWords.english.length)
                    this.wordList.push(this.randomWords.english[n]);
                    console.log(this.randomWords.english[n]);
                }
                console.log(this.wordList.length);
            }
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
            width: 65%
        }

        .textarea {
            width: 78%;
        }

        .redo-trigger {
            width: 20%;
        }
    }

</style>