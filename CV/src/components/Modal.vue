<template>
        <div ref="modal">
            <p>Link is copied to Clipboard</p>
        </div>
</template>

<script>
    export default {
        name: "Modal",
        props: ['y'],
        mounted() {
            this.$refs.modal.style.top = this.y + window.pageYOffset - 400 +  'px'
        }
    }
</script>

<style scoped lang="scss">
    div {
        min-height: min-content;
        /*height: 100px;*/
        min-width: min-content;
        width: 40vw;
        position: absolute;
        z-index: 100;
        text-align: center;
        background-color: rgb(149, 149, 149);
        border-radius: 5px;
        margin: auto;
        left: 0;
        right: 0;
        padding: 20px;

        p {
            font-family: monospace;
            font-size: 1.5rem;
        }
    }
</style>