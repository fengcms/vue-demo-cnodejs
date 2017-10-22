<template>
  <div class="keyboard">
    <h1>键盘编辑</h1>
    <div class="keyboard_control">
      <button class="add_key" @click="addKey()">添加一个按键</button>
      <button class="remove_key" @click="removeKey()">删除一个按键</button>
      <button class="clean_key" @click="cleanKey()">清空所有按键</button>
      <button class="save_key" @click="saveKey()">保存设定</button>
      <br>
      <button class="key_type" :class="{'curl':keyboardType === 21}" @click="setKeyBoardType(21, 'key104')">104键盘</button>
      <button class="key_type" :class="{'curl':keyboardType === 17}" @click="setKeyBoardType(17, 'key84')">84键盘</button>
      <button class="key_type" :class="{'curl':keyboardType === 14}" @click="setKeyBoardType(14, 'key60')">60键盘</button>
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
import keyboard from '@/utils/keyboard.json'
export default {
  data () {
    return {
      key: [],
      curlIndex: null,
      keyboardType: 21,
      curlKey: {
        width: null,
        height: null,
        left: null,
        top: null,
        text: new Array(11)
      }
    }
  },
  created () {
    document.title = 'Keyboard Layout Editor'
    if (localStorage.getItem('key')) {
      this.key = JSON.parse(localStorage.getItem('key'))
    }
  },
  methods: {
    getStyle (o) {
      return 'left:' + o.left * 56 + 'px; top:' + o.top * 56 + 'px;width: ' + o.width * 56 + 'px;height: ' + o.height * 56 + 'px;'
    },
    addKey () {
      let left = null
      let top = null
      if (this.key.length === 0) {
        left = 0
        top = 0
      } else {
        let lastKey = this.getLastKey()
        if (lastKey.left >= this.keyboardType) {
          left = 0
          top = +lastKey.top + 1
        } else {
          left = +lastKey.left + +lastKey.width
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
      this.curlIndex = this.key.length - 1
      this.curlKey = this.key[this.curlIndex]
    },
    getLastKey () {
      let o = this.key.length > 0 ? this.key[0] : this.normalKey()
      for (var i = 0; i < this.key.length; i++) {
        let k = this.key[i]
        if (k.top > o.top) {
          o = k
        } else if (k.left > o.left) {
          o = k
        }
      }
      return o
    },
    removeKey () {
      delete this.key[this.curlIndex]
      this.key = this.key.filter(function (n) { return n })
      this.curlIndex = this.key.length - 1 < this.curlIndex ? this.key.length - 1 : this.curlIndex
      this.curlKey = this.key.length > 0 ? this.key[this.curlIndex] : this.normalKey()
    },
    chooseCurlKey (index) {
      this.curlIndex = index
      this.curlKey = this.key[index]
    },
    normalKey () {
      let o = {
        width: null,
        height: null,
        left: null,
        top: null,
        text: new Array(11)
      }
      return o
    },
    cleanKey () {
      this.key = []
      this.curlIndex = null
      this.curlKey = this.normalKey()
    },
    setKeyBoardType (w, type) {
      w = +w
      this.keyboardType = w
      this.key = keyboard[type]
    },
    saveKey () {
      localStorage.setItem('key', JSON.stringify(this.key))
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
