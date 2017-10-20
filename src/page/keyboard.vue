<template>
  <div class="keyboard">
    <h1>键盘编辑</h1>
    <div class="keyboard_control">
      <button class="add_key" @click="addKey()">添加一个按键</button>
      <button class="remove_key" @click="removeKey()">删除一个按键</button>
    </div>
    <div class="keyboard_edit">
      <div class="keyboard_layout">
        <div class="key" v-for="i,k in key" :class="{'curl':k === curlIndex}" :style="getStyle(i)" @click="chooseCurlKey(k)">
          <div class="key_hat">
            <span class="text text_1 text_l" v-text="i.text[0]"></span>
            <span class="text text_1 text_m" v-text="i.text[1]"></span>
            <span class="text text_1 text_r" v-text="i.text[2]"></span>
            <span class="text text_2 text_l" v-text="i.text[3]"></span>
            <span class="text text_2 text_m" v-text="i.text[4]"></span>
            <span class="text text_2 text_r" v-text="i.text[5]"></span>
            <span class="text text_3 text_l" v-text="i.text[6]"></span>
            <span class="text text_3 text_m" v-text="i.text[7]"></span>
            <span class="text text_3 text_r" v-text="i.text[8]"></span>
            <span class="text text_4 text_l" v-text="i.text[9]"></span>
            <span class="text text_4 text_m" v-text="i.text[10]"></span>
            <span class="text text_4 text_r" v-text="i.text[11]"></span>
          </div>
        </div>
      </div>
    </div>
    <div class="keyboard_params">
      <dl>
        <dt>宽度：</dt>
        <dd><input type="number" v-model="curlKey.width" step="0.25"></dd>
      </dl>
      <dl>
        <dt>高度：</dt>
        <dd><input type="number" v-model="curlKey.height" step="0.25"></dd>
      </dl>
      <dl>
        <dt>左边距：</dt>
        <dd><input type="number" v-model="curlKey.left" step="0.25"></dd>
      </dl>
      <dl>
        <dt>上边距：</dt>
        <dd><input type="number" v-model="curlKey.top" step="0.25"></dd>
      </dl>
      <dl>
        <dt>顶行文字：</dt>
        <dd>
          <input type="text" v-model="curlKey.text[0]">
          <input type="text" v-model="curlKey.text[1]">
          <input type="text" v-model="curlKey.text[2]">
        </dd>
      </dl>
      <dl>
        <dt>中行文字：</dt>
        <dd>
          <input type="text" v-model="curlKey.text[3]">
          <input type="text" v-model="curlKey.text[4]">
          <input type="text" v-model="curlKey.text[5]">
        </dd>
      </dl>
      <dl>
        <dt>底行文字：</dt>
        <dd>
          <input type="text" v-model="curlKey.text[6]">
          <input type="text" v-model="curlKey.text[7]">
          <input type="text" v-model="curlKey.text[8]">
        </dd>
      </dl>
      <dl>
        <dt>侧边文字：</dt>
        <dd>
          <input type="text" v-model="curlKey.text[9]">
          <input type="text" v-model="curlKey.text[10]">
          <input type="text" v-model="curlKey.text[11]">
        </dd>
      </dl>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      key: [
        {
          width: 1,
          height: 1,
          left: 0,
          top: 0,
          text: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
        }
      ],
      curlIndex: 0,
      curlKey: {
        width: 1,
        height: 1,
        left: 0,
        top: 0,
        text: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
      }
    }
  },
  created () {
    // this.getData()
  },
  methods: {
    getStyle (o) {
      return 'left:' + o.left * 56 + 'px; top:' + o.top * 56 + 'px;width: ' + o.width * 56 + 'px;height: ' + o.height * 56 + 'px;'
    },
    addKey () {
      console.log(JSON.stringify(this.key))
      let left = null
      let top = null
      let lastKeyIndex = this.key.length - 1
      let lastKey = this.key[lastKeyIndex]
      if (lastKeyIndex === -1) {
        left = 0
        top = 0
      } else {
        if (lastKey.left === 14) {
          left = 0
          top = +lastKey.top + 1
        } else {
          left = +lastKey.left + 1
          top = lastKey.top
        }
      }
      this.key.push({
        width: 1,
        height: 1,
        left: left,
        top: top,
        text: new Array(11)
      })
    },
    removeKey () {
      // console.log(JSON.stringify(this.key))
      delete this.key[this.curlIndex]
      console.log(this.curlIndex)
      console.log(this.key.length - 1)
      if (this.curlIndex === this.key.length - 1) { this.curlIndex -= 1 }
      console.log(this.curlIndex)
      this.key = this.key.filter(function (n) { return n })
      this.curlKey = this.key[this.curlIndex]
    },
    chooseCurlKey (index) {
      this.curlIndex = index
      this.curlKey = this.key[index]
    }
  },
  watch: {
    curlKey: {
      handler: function (val, oldVal) {
        this.key[this.curlIndex] = this.curlKey
      },
      deep: true
    }
  }
}
</script>
