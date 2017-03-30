<template>
    <div class="main-info" id="start">
        <h2>ImagePreivewer 选择文件并预览</h2>
        <p class="mark-p">功能组件</p>

        <div class="codebox">
            <div class="codetitle">
                <span>基础用法</span>
            </div>

            <div class="codecontent">
                <div class="codeabout">
                    <div class="spa">基础的 `ImagePreivewer` 用法。</div>
                    <ImagePreviewer v-model="image"></ImagePreviewer>
                    <hr>
                    <div>
                        您的`image`的`src` 为：{{ image }}
                        <br>
                        解码后：{{ escapedURI }}
                    </div>
                </div>
            </div>
        </div>

        <h2>Code</h2>
        <p class="mark-p">组件实现的代码 （ 其中包括了 html、less、js ） </p>
        <div class="codebox">
            <div class="codetitle">
                <span>Code</span>
            </div>
            <div class="codecontent">
                <div class="codeabout">
                    <codeBlock :code="codeButton"></codeBlock>
                </div>
            </div>
        </div>

        <h2>API</h2>
        <p class="mark-p">我们提供了基本的API ( 里面主要包括了 props、 slot、 event ) </p>
        <table class="api-table">
            <thead>
                <tr>
                    <td>属性</td>
                    <td>说明</td>
                    <td>类型</td>
                    <td>可选值</td>
                    <td>默认值</td>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>iconType</td>
                    <td>图标类型</td>
                    <td>String</td>
                    <td></td>
                    <td>upload</td>
                </tr>
            </tbody>
        </table> 
    </div>
</template>

</template>

<script>
    import codeBlock from '../components/codeBlock'
    import codeButton from '!raw!../components/func/image-previewer'

    import ImagePreviewer from '../components/func/image-previewer'

    export default {
        name: 'backTop',
        components: {
            codeBlock,
            ImagePreviewer
        },
        data () {
            return {
                codeButton,
                image: ''
            }
        },
        computed: {
            escapedURI () {
                return window.unescape(this.image)
            }
        }
    }
</script>

<style lang="less" scoped>

</style>
