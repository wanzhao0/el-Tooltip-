<template>
    <el-tooltip ref="tlp" :content="text" effect="dark" :disabled="!tooltipFlag" :placement="placement" class="tooltip">
        <span :class="className"
            @mouseenter="visibilityChange($event)">{{ text | visibilityText(maxTextLength) }}</span>
    </el-tooltip>
</template>

<script>
    export default {
        name: 'ellipsisTooltip',
        props: {
            text: { type: String, default: '' }, // 字符内容
            placement: { type: String, default: 'top-start' },
            className: { type: String, default: 'text' }, // class
            disabledTip: { type: Boolean, default: true }, // 是否hover显示
            maxTextLength: { type: Number, default: 100 } // 文字最大长度,超过截取字符
        },
        data() {
            return {
                tooltipFlag: false
            }
        },
        methods: {
            // tooltip的可控
            visibilityChange(event) {
                if (!this.disabledTip) { //是否显示
                    return false
                }
                const ev = event.target
                const ev_height = ev.offsetHeight // 文本的实际高度
                const content_height = this.$refs.tlp.$el.parentNode.clientHeight // 文本容器高度
                if (content_height < ev_height) {
                    // 实际内容高度 > 文本高度 =》内容溢出
                    this.tooltipFlag = true // NameIsIncludeWord ? true : !!false
                } else {
                    // 否则为不溢出
                    this.tooltipFlag = false
                }
            }
        },
        filters: {
            visibilityText(val, maxTextLength) {
                if (val && val.length) {
                    return val.length > maxTextLength ? val.substring(0, maxTextLength) + '...' : val;
                } else {
                    return ''
                }
            }
        }
    }
</script>
<style scoped>
    /* // el-tooltip二次封装 */
    .tooltip {
        height: 16px;
        /* 必须要有高度设置，因为tooltip的显示条件是通过高度来判断的 */
        /* display: inline-block;
        display: -webkit-box; */
        -webkit-line-clamp: 1;
        /*因为通过高度所以只显示一行，溢出显示省略号*/
        -webkit-box-orient: vertical;
        overflow: hidden;
        text-overflow: ellipsis;
        word-break: break-all;
    }

    /*英文数字折行*/
    .tooltip span {
        line-height: 1.3;
        /*这个行高看自定义样式文本高度*/
    }
</style>