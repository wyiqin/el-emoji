<template>
  <el-popover
    slot="suffix"
    v-model="visible"
    :placement="placement"
    trigger="click"
  >
    <div class="el-emoji-opt">
      <el-tabs v-model="activeTab">
        <el-tab-pane v-for="(group, index) in options" :key="group.name" :label="group.name" :name="index + ''">
          <ul class="el-emoji-opt-list">
            <li v-for="item in group.list" :key="item.value">
              <img class="el-emoji-opt-item" :src="item.img" :alt="item.value" @click="appendEmoji(item)">
            </li>
          </ul>
        </el-tab-pane>
      </el-tabs>
    </div>
    <div slot="reference" class="el-emoji-opt-btn">
      <slot />
    </div>
  </el-popover>
</template>

<script>
export default {
  props: {
    placement: {
      type: String,
      default: 'bottom-start'
    },
    options: {
      type: Array,
      default: () => {
        return [
          {
            name: '小黄脸',
            list: [
              {
                value: '微笑',
                img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f603.svg'
              },
              {
                value: '哈哈',
                img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f604.svg'
              },
              {
                value: '流汗',
                img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f605.svg'
              },
              {
                value: '惊喜',
                img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f606.svg'
              },
              {
                value: '天使',
                img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f607.svg'
              },
              {
                value: '恶魔',
                img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f608.svg'
              },
              {
                value: '眨眼',
                img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f609.svg'
              },
              {
                value: '呆了',
                img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f610.svg'
              }
            ]
          }
        ]
      }
    }
  },
  data() {
    return {
      visible: false,
      activeTab: '0'
    }
  },
  methods: {
    appendEmoji(item) {
      this.visible = false
      this.$emit('append', item)
    }
  }
}
</script>

<style lang="scss" scoped>
  .el-emoji-opt {
    height: 234px;
    width: 304px;
    font-size: 0;
    overflow: auto;
    .el-emoji-opt-list {
      height: 180px;
      padding: 0px;
      list-style: none;
      li {
        float: left;
      }
      .el-emoji-opt-item {
        margin: 4px;
        width: 24px;
        height: 24px;
        &:hover {
          background-color: #ddd;
        }
      }
    }
  }
  .el-emoji-opt-btn {
    display: inline-block;
  }

</style>
