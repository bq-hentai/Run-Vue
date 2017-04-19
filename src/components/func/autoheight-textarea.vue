<template>
    <div
        class="elm"
        :class="{ 'pre': pre }"
        :contenteditable="contenteditable"
        :pre="pre"
        @input="handleInput"
    >
    </div>
</template>

<script>
    export default {
        name: 'AutoheightTextarea',
        props: {
            value: {
                type: String,
                default () {
                    return ''
                }
            },
            contenteditable: {
                type: Boolean,
                default () {
                    return true
                }
            },
            pre: {
                type: Boolean,
                default () {
                    return true
                }
            }
        },
        watch: {
            value (value) {
                /* prevent cursor change */
                if (value !== this.$el.innerText) {
                    this.$el.innerText = value
                }
            }
        },
        methods: {
            handleInput () {
                this.$emit('input', this.$el.innerText)
            }
        },
        mounted () {
            this.$el.innerText = this.value
        }
    }
</script>

<style lang="less">
    .elm {
        width: calc(100% - 114px);
        min-height: 120px;
        height: auto;
        padding: 0 1em 0 1em;
        background-color: #fff;
        /* prevent focus explosion <_< */
        outline: none;
        float: right;
        cursor: text;
    }

    .pre {
        white-space: pre-wrap;
        word-break: break-all;
    }
</style>
