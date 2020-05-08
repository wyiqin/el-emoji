<template>
  <div>
    <el-input v-model="data">
      <el-popover
        v-model="visible"
        slot="suffix"
        placement="bottom"
        trigger="click">
        <!-- emoji select conment-->
        <div class="el-emoji-conment">
          <!-- tabs -->
          <el-tabs v-model="activeTab" >
            <el-tab-pane v-for="(group, index) in options" :key="group.name" :label="group.name" :name="index + ''">
              <ul class="el-emoji-list">
                <li v-for="item in group.list" :key="item.value">
                  <img @click="appendEmoji(item)" class="el-emoji-item" :src="item.img" :alt="item.value">
                </li>
              </ul>
            </el-tab-pane>
          </el-tabs>
        </div>
        <span slot="reference">
          <i class="el-emoji-btn el-input__icon el-icon-picture-outline-round"></i>
        </span>
      </el-popover>
    </el-input>
  </div>
</template>

<script>
export default {
  name: 'ElEmojiInput',
  props: {
    value: {
      type: String,
      default: ''
    },
    options : {
      type: Array,
      default: ()=> {
         return [
        {
          name: '小黄脸',
          list: [
            {
              value :'微笑',
              img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f603.svg'
            },
            {
              value :'哈哈',
              img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f604.svg'
            },
            {
              value :'流汗',
              img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f605.svg'
            },
            {
              value :'惊喜',
              img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f606.svg'
            },
            {
              value :'天使',
              img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f607.svg'
            },
            {
              value :'恶魔',
              img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f608.svg'
            },
            {
              value :'眨眼',
              img: 'https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f609.svg'
            },
            {
              value :'呆了',
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
      activeTab: 0,
      visible: false,
    }
  },
  filters: {
    formatEmoji(val) {
      val = val.replace(/\[哈哈\]/g,'🙄')
      console.log(val);
      
      return val
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
  },
  mounted() {
  },
  methods: {
    appendEmoji(item) {
      this.visible = false
      this.data = this.data + `[${item.value}]`
    }
  }
};
</script>
<style lang="scss" scoped>
  .el-emoji-conment {
    height: 234px;
    width: 304px;
    font-size: 0;
    overflow: auto;
    .el-emoji-list {
      height: 180px;
      padding: 0px;
    }
  }
  .el-emoji-btn {
    &:hover {
      color: #606266;
    }
  }
  .el-emoji-list {
    list-style: none;
    li {
      float: left;
    }
  }
  .el-emoji-item {
    margin: 4px;
    width: 24px;
    height: 24px;
    &:hover {
      background-color: #ddd;
    }
  }
</style>