<template>
    <div class="edit-area">
      <vue-ueditor v-bind:value=defaultMsg v-bind:config=config v-on:input="input" v-on:ready="ready"></vue-ueditor>
    </div>
</template>

<script>
import vueUeditor from './vueUeditor'
export default {
  name: 'hello',
  data () {
    return {
      defaultMsg: '初始文本',
      //传入百度编辑器变量可设置百度编辑器样式
      config: {
        initialFrameWidth: null,//编辑器宽度
        initialFrameHeight: 200,//编辑器高度
          scaleEnabled:true，//百度编辑器自动显示滚动条
      }
    }
  },
  components: {
    vueUeditor
  },
  methods: {
    ready(UeditorInstance){
      console.log(UeditorInstance)
    },
    input(obj){
        console.log(obj);
    }
  },
  mounted(){
  }
}
</script>

<style scoped>
<!--css -->
</style>