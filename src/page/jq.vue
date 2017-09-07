<template>
  <div class="love">
    <p>这里是初始文字</p>
    <button @click="testJQ">看看 jquery 有没有工作</button>
  </div>
</template>
<script>
export default {
  methods: {
    testJQ () {
      $('.love p').html('jquery 工作正常！')
    }
  }
}
</script>
