<template>
    <div class="area my-auto flex justify-center items-center">
        <div class="main-type bg-teal-200 p-8 rounded-lg">
            <div class="text-display mb-4 text-blue-800 text-2xl font-semibold">program own write like hold form who follow must between course few little move how get system few just be you or turn need</div>
            <div class="flex justify-between">
                <input v-model="inputWord" type="text" name="" id="" class="textarea p-3 bg-teal-600 text-white rounded-lg border-teal-600 outline-none focus:border-teal-400 border-8 text-2xl">
                <button class="redo-trigger bg-blue-800 hover:bg-blue-500 text-white font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded text-xl" v-if="timer == 0">Redo</button>
                <span class="redo-trigger bg-blue-800 text-white font-semibold border border-blue-500 rounded text-xl" v-if="timer != 0">{{ timer }}</span>
            </div>
            <span class="redo-trigger bg-blue-800 text-white font-semibold border border-blue-500 rounded text-xl" v-if="timer != 0">{{ inputWord }}</span>

        </div>
    </div>
</template>

<script>
    export default {
        name: "typearea",

        data () {
            return {
                // message,
                inputWord: '',
                timer: 60
            }
        },


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