<template>
    <div class="flex justify-center bg-teal-600 font-mono nav">
        <img src="../assets/images/typeherologowhite.svg" alt="logo">
    </div>
</template>

<script>
export default {
    name: "navbar",
    props: {
        msg: String
    }
};
</script>

<style lang="scss" scoped>
    .nav {
        height: 15%;
    }
</style>
