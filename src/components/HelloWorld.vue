<template>
  <div class="hello">
    <h1>emoji😄</h1>
    <hr><br>
    <label>展示：</label><br>
    <el-emoji-warp emoji-class-name="abc" :content="input" />
    <br><br>
    <label>输入框：</label>
    <el-emoji-input v-model.lazy="input" />
    <p style="font-size:10px">插槽</p>
    <el-emoji-input>
      <el-input v-model="input" size="mini" />
    </el-emoji-input>
    <br>
    <label>文本域：</label>
    <el-emoji-input v-model.lazy="input" type="textarea" />
    <p style="font-size:10px">插槽</p>
    <el-emoji-input>
      <el-input v-model="input" type="textarea" maxlength="100" show-word-limit />
    </el-emoji-input>
    <br><hr><br>
    <label>选择框：</label><br>
    <!-- $attrs 传入属性，事件emit -->
    <el-emoji-select v-model="select" clearable placeholder="请选择" />
    <br>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  components: {
    'el-emoji-input': () => import('./input.vue'),
    'el-emoji-select': () => import('./select.vue'),
    'el-emoji-warp': () => import('./wrap')
  },
  data() {
    return {
      input: '你好饿了么[哈哈]',
      select: '',
      value: 1,
      iconClasses: ['icon-rate-face-off', 'el-icon-picture-outline-round', 'el-icon-picture-outline-round'] // 等同于 { 2: 'icon-rate-face-1', 4: { value: 'icon-rate-face-2', excluded: true }, 5: 'icon-rate-face-3' },

    }
  }
}
</script>
<style lang="scss">
.abc {
  &:hover {
    -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6);
    box-shadow: inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6)
  }
  border-bottom: 1px dashed;
}
</style>>

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
