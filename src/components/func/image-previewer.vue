<template>
    <div class="wrapper">
        <input type="file" @change="handleChange" class="file-selector">
        <div class="presenter" @click="handlePresenterClick">
            <uiIcon :name="iconType || 'upload'"></uiIcon>
            <slot></slot>
        </div>
        <div class="image-content"></div>
    </div>
</template>

<script>
    import uiIcon from '../base/icon'

    const URL$ = window.URL

    export default {
        name: 'ImagePreviewer',
        data () {
            return {
                previousUrl: ''
            }
        },
        components: {
            uiIcon
        },
        props: {
            value: {
                type: String,
                default () {
                    return ''
                }
            },
            iconType: {
                type: String,
                default () {
                    return ''
                }
            }
        },
        methods: {
            handleChange (evt) {
                if (this.previousUrl) {
                    // don't forget revoke
                    URL$.revokeObjectURL(this.previousUrl)
                }
                const files = [ ...evt.target.files ]
                const file = files[0]
                // repeat
                evt.target.value = null

                const url = URL$.createObjectURL(file)
                this.previousUrl = url
                this.createImage(url)
                this.$emit('input', url)
            },
            handlePresenterClick () {
                // for IE9+
                this.$el.querySelector('.file-selector').click()
            },
            createImage (src) {
                this.$el.querySelector('.image-content').innerHTML = `<img src="${src}">`
            }
        }
    }
</script>

<style lang="less">
    .wrapper {
        position: relative;

        .file-selector {
            /*
             * use opacity can save many codes but then we can't see hand
             * opacity: 0;
             * position: absolute;
             * top: 0;
             * right: 0;
             * bottom: 0;
             * left: 0;
             */
            display: none;
        }

        .presenter {
            display: inline-block;
            cursor: pointer;
        }

        .image-content {
            width: 200px;
        }
    }
</style>
