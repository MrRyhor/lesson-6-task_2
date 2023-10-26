<template>
    <src-input v-model:source.checkPath="sourceJS" />    
</template>

<script>
import SrcInput from './components/SrcInput.vue'

export default {
    name: 'App',

    components: {
        SrcInput,
    },

    data() {
        return {
            sourceJS: null,
        }
    },
}
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
