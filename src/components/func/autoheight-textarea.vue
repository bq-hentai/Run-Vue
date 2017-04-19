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
        width: 150px;
        min-height: 50px;
        height: auto;
        padding: 1em;
        border: 1px solid #eee;
        border-radius: 2px;
        background-color: red;
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
