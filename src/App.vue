<template>
    <MainPage/>
</template>

<script>
    import MainPage from './components/MainPage.vue'

    export default {
        components: {MainPage}
    }
</script>

<style lang="scss">
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
        &::-webkit-scrollbar {
            width: 10px;
        }

        &::-webkit-scrollbar-track {
            background-color: #2b2b2b;
        }

        &::-webkit-scrollbar-thumb {
            background-color: #4e4e4e;
        }
    }
</style>