<template>
    <div class="area my-auto flex justify-center items-center">
        <div class="main-type bg-blue-200 p-8 rounded-lg">
            <div class="text-display mb-4">program own write like hold form who follow must between course few little move how get system few just be you or turn need</div>
            <div class="flex justify-between">
                <input type="text" name="" id="" class="textarea p-3 bg-teal-600 text-white">
                <button class="redo-trigger bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded">Redo</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "typearea"
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