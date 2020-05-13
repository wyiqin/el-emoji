<template>
  <div>
    <div v-if="mytype === 'input'">
      <slot>
        <el-input v-model="data">
          <options slot="suffix" placement="bottom-end" @append="append">
            <i class="el-emoji-btn el-input__icon el-icon-picture-outline-round" />
          </options>
        </el-input>
      </slot>
      <span v-if="$slots.default" ref="suffix" class="el-input__suffix">
        <span class="el-input__suffix-inner">
          <options slot="suffix" placement="bottom-end" @append="append">
            <i data-v-45dba22c class="el-emoji-btn el-input__icon el-icon-picture-outline-round" />
          </options>
        </span>
      </span>
    </div>
    <div v-else>
      <slot>
        <el-input v-model="data" type="textarea" />
      </slot>
      <options @append="append">
        <el-button style="margin-top:3px" size="mini" icon="el-icon-picture-outline-round">表情</el-button>
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
    },
    mytype() {
      if (this.$slots.default) {
        return this.$slots.default[0].componentOptions.propsData.type || 'input'
      } else {
        return this.type
      }
    }
  },
  mounted() {
    if (this.$slots.default && this.mytype === 'input') {
      this.$slots.default[0].elm.append(this.$refs.suffix)
    }
  },
  methods: {
    append(item) {
      if (this.$slots.default) {
        this.$slots.default[0].componentInstance.$emit('input', this.$slots.default[0].componentInstance.value + `[${item.value}]`)
      } else {
        this.data += `[${item.value}]`
      }
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
