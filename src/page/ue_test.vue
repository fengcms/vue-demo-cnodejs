<template>
  <div>
    <Uediter :value="ueditor.value" :config="ueditor.config" ref="ue"></Uediter>
    <input type="button" value="显示编辑器内容（从控制台查看）" @click="returnContent">
  </div>
</template>
<script>
  import Uediter from '@/components/ue.vue'
  export default {
    components: {Uediter},
    data () {
      return {
        dat: {
          content: ''
        },
        ueditor: {
          value: '编辑器默认文字',
          config: {}
        }
      }
    },
    methods: {
      returnContent () {
        this.dat.content = this.$refs.ue.getUEContent()
        console.log(this.dat.content)
      }
    }
  }
</script>
