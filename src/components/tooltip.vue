<template>
    <div ref="tooltip">
        <p>
            1+ year
        </p>
    </div>
</template>

<script>
    export default {
        name: "tooltip",
        props: ['x', 'y'],
        emits: ['visible'],
        watch: {
            x() {
                this.$emit('visible')
                this.$refs.tooltip.style.left = (this.x + 25) + 'px'
            },
            y() {
                this.$emit('visible')
                this.$refs.tooltip.style.top = (this.y - 75) + 'px'
            }
        }
    }
</script>

<style scoped lang="scss">
    div {
        position: absolute;
        border: #2BCC0B 1px solid;
        padding: 10px;
        background-color: rgb(149, 149, 149);
        font-size: 1.4rem;
        font-family: monospace;
        z-index: 100;
    }
</style>