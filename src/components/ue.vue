<template>
  <div>
    <script id="editor" type="text/plain"></script>
  </div>
</template>
<script>
  export default {
    name: 'ue',
    data () {
      return {
        editor: null
      }
    },
    props: {
      value: '',
      config: {}
    },
    mounted () {
      const _this = this
      this.editor = window.UE.getEditor('editor', this.config)
      this.editor.addListener('ready', function () {
        _this.editor.setContent(_this.value)
      })
    },
    methods: {
      getUEContent () {
        return this.editor.getContent()
      }
    },
    destroyed () {
      this.editor.destroy()
    }
  }
</script>
