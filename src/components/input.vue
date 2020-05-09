<template>
  <div>
    <el-input v-if="type === 'input'" v-model="data">
      <options slot="suffix" placement="bottom-end" @append="append">
        <i class="el-emoji-btn el-input__icon el-icon-picture-outline-round" />
      </options>
    </el-input>
    <div v-else>
      <el-input v-model="data" type="textarea" />
      <options @append="append">
        <el-button size="mini" icon="el-icon-picture-outline-round">表情</el-button>
      </options>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ElEmojiInput',
  components: {
    options: () => import('./options')
  },
  filters: {
    formatEmoji(val) {
      val = val.replace(/\[哈哈\]/g, '🙄')
      console.log(val)

      return val
    }
  },
  props: {
    value: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'input'
    }
  },
  data() {
    return {
      activeTab: 0,
      visible: false
    }
  },
  computed: {
    data: {
      get: function() {
        return this.value
      },
      set: function(v) {
        this.$emit('input', v)
      }
    }
  },
  mounted() {
  },
  methods: {
    append(item) {
      this.data = this.data + `[${item.value}]`
    }
  }
}
</script>
<style lang="scss" scoped>
.el-emoji-btn {
  &:hover {
    color: #606266;
  }
}
</style>
