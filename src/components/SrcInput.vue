<template>
    <div>
        <label
            >Please enter src https//:
            <input ref="inp" type="text" v-model="checkSrc" />
        </label>
        <button v-if="btnVisible" type="button" @click="clearInput">Clear Input</button>
    </div>
</template>
<script>
export default {
    name: 'SrcInput',

    props: {
        source: { type: String },
        sourceModifiers: { default: () => ({}) },
    },

    data() {
        return {
            btnVisible: false,
        }
    },

    computed: {
        checkSrc: {
            get() {
                return this.source
            },
            set(val) {
                let res = this.getRegexVal(val)
                if (res) {
                    val = String(val.match(/\w+\.js/g))
                    this.$refs.inp.disabled = true
                    this.btnVisible = true
                }
                this.$emit('update:source', val)
                if (val && this.sourceModifiers.checkPath) this.setBGColor(val)
            },
        },
    },
    methods: {
        setBGColor(val) {
            let res = this.getRegexVal(val)
            if (!res) this.$refs.inp.style.backgroundColor = 'red'
            else this.$refs.inp.style.backgroundColor = 'transparent'
        },
        getRegexVal(val) {
            return /\w+\.js/g.test(val)
        },
        clearInput() {
            this.$refs.inp.style.backgroundColor = 'transparent'
            this.$refs.inp.disabled = false
            this.$refs.inp.focus()
            this.btnVisible = false
            this.$nextTick(() => (this.$refs.inp.value = ''))
        },
    },
}
</script>
<style lang="scss" scoped></style>
