<template>
  <div>
    <p>{{'大哥一打三真滴[哈哈]6[哈哈]' | formatEmoji}}</p>
    <hr>
    <el-input v-model="value">
      <el-popover
        v-model="visible"
        slot="suffix"
        placement="bottom"
        title="标题"
        width="200"
        trigger="click">
        <div>
          <img @click="img1" class="el-emoji" src="https://i0.hdslb.com/bfs/emote/3ad2f66b151496d2a5fb0a8ea75f32265d778dd3.png@112w_112h.webp" alt="图">
        </div>
        <!-- <el-button type="text" slot="reference"> -->
          <i slot="reference"  class="el-emoji-btn el-input__icon el-icon-picture-outline-round"></i>
        <!-- </el-button> -->
      </el-popover>
    </el-input>
  </div>
</template>

<script>
export default {
  data() {
    return {
      visible: false,
      value: '你好'
    }
  },
  filters: {
    formatEmoji(val) {
      val = val.replace(/\[哈哈\]/g,'🙄')
      console.log(val);
      
      return val
    }
  },
  mounted() {
  },
  methods: {
    img1() {
      this.visible = false
      this.value = this.value + '[哈哈]'
    }
  }
};
</script>
<style lang="scss" scoped>
  .el-emoji-btn {
    &:hover {
      color: red;
    }
  }
  .el-emoji {
    margin: 4px;
    width: 24px;
    height: 24px;
    &:hover {
      background-color: #ddd;
    }
  }
</style>