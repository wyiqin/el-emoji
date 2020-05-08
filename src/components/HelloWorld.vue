<template>
  <div class="hello">
    <h1>emoji😄</h1>
    <hr><br>
    <label>展示：</label><br>
    <el-emoji-warp :content="input" />
    <br><br>
    <label>输入：</label>
    <el-emoji-input v-model.lazy="input"></el-emoji-input>
    <br><hr><br>
    <label>选择框：</label><br>
    <el-emoji-select v-model="select"></el-emoji-select>
    <br>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      input: '你好饿了么[哈哈]',
      select: '',
      value: 1,
      iconClasses: ['icon-rate-face-off', 'el-icon-picture-outline-round', 'el-icon-picture-outline-round'] // 等同于 { 2: 'icon-rate-face-1', 4: { value: 'icon-rate-face-2', excluded: true }, 5: 'icon-rate-face-3' },
      
    }
  },
  components: {
    'el-emoji-input': () => import('./input.vue'),
    'el-emoji-select': () => import('./select.vue'),
    'el-emoji-warp': () => import('./wrap'),
  },
  props: {
    msg: String
  }
}
</script>

<style scoped>
.hello {
  width: 400px;
  border: 1px solid #eee;
  padding: 0 20px;
  margin: 0 auto;
  position: relative;
}
hr {
  background: #c0c4cc;
  border: 0;
  height: 1px;
}
label {
  display: inline-block;
  margin-bottom: 5px;
}
</style>