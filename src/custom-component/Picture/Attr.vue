<template>
    <div class="attr-list">
        <CommonAttr></CommonAttr>
        <el-form>
            <el-form-item label="镜像翻转">
                <div style="clear: both;">
                    <el-checkbox v-model="curComponent.propValue.flip.horizontal" label="horizontal">水平翻转</el-checkbox>
                    <el-checkbox v-model="curComponent.propValue.flip.vertical" label="vertical">垂直翻转</el-checkbox>
                </div>
            </el-form-item>
            <el-form-item label="插入图片">
                <div class="avatar el-icon-upload el-icon--right">
                    <input
                        type="file"
                        @change="getObjectURL">
                    上传图片
                </div>
            </el-form-item>
        </el-form>
    </div>
</template>

<script>
import CommonAttr from '@/custom-component/common/CommonAttr.vue'

export default {
    components: { CommonAttr },
    computed: {
        curComponent() {
            return this.$store.state.curComponent
        },
    },
    methods: {
        getObjectURL(e) {
            let url = null
            if (window.createObjcectURL != undefined) {
                url = window.createOjcectURL(e.target.files[0])
            } else if (window.URL != undefined) {
                url = window.URL.createObjectURL(e.target.files[0])
            } else if (window.webkitURL != undefined) {
                url = window.webkitURL.createObjectURL(e.target.files[0])
            }
            this.curComponent.propValue.url = url
        },
    },
}
</script>
<style lang="scss" scoped>
.attr-list {
    overflow: auto;
    padding: 20px;
    padding-top: 0;
    height: 100%;
}

.avatar {
    position: relative;
    display: block;
    overflow: hidden;
    width: 100%;
    height: 34px;
    line-height: 34px;
    border: 1px solid #99D3F5;
    border-radius: 4px;
    text-align: center;
    background: #409eff;
    color:white;
    cursor: pointer;
     :hover{

     }
}

.avatar input {
    display: inline-block;
    // 设置input绝对定位，后面的文字才能往上移动
    position: absolute;
    font-size: 12px;
    top: 0;
    left: 0;
    // 将原来的input变透明
    opacity: 0;
    z-index: 1;
    cursor: pointer;
}
</style>
