<template>
  <div class="hello">
    <h1>emoji😄</h1>
    <hr><br>
    <label>输入：</label>
    <el-emoji-input v-model="input"></el-emoji-input>
    <br>
    <label>展示：</label><br>
    <el-emoji-warp :content="input" />
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      input: '你好饿了么[哈哈]'
    }
  },
  components: {
    'el-emoji-input': () => import('./input.vue'),
    'el-emoji-warp': () => import('./wrap'),
  },
  props: {
    msg: String
  }
}
</script>

<style scoped>
.hello {
  width: 300px;
  height: 500px;
  border: 1px solid #eee;
  padding: 5px;
  margin: 0 auto;
}
</style>
