<template>
<div class="el-emoji-select">
  <div class="el-select__tags el-emoji-warp">
    <el-emoji-warp :content="data"></el-emoji-warp>
  </div>
  <el-select
    v-model="data"
    reserve-keyword
    clearable
    :placeholder="currentPlaceholder">
    <el-option
      v-for="item in eOptions"
      :key="item.value"
      label=" "
      :value="'['+item.value+']'">
      <span style="float: left">
        <img class="el-emoji-item" :src="item.img" :alt="item.value"/>
      </span>
      <span style="float: right">{{item.value}}</span>
    </el-option>
  </el-select>
  </div>
</template>

<script>
const list = [
  {
    value: "微笑",
    img: "https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f603.svg"
  },
  {
    value: "哈哈",
    img: "https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f604.svg"
  },
  {
    value: "流汗",
    img: "https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f605.svg"
  },
  {
    value: "惊喜",
    img: "https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f606.svg"
  },
  {
    value: "天使",
    img: "https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f607.svg"
  },
  {
    value: "恶魔",
    img: "https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f608.svg"
  },
  {
    value: "眨眼",
    img: "https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f609.svg"
  },
  {
    value: "呆了",
    img: "https://gold-cdn.xitu.io/asset/twemoji/2.6.0/svg/1f610.svg"
  }
];

export default {
  name: 'ElEmojiSelect',
  components: {
    'el-emoji-warp': () => import('./wrap'),
  },
  props: {
     value: {
      type: String,
      default: ''
    },
    options : {
      type: Array,
      default: ()=> {
         return ['天使','恶魔']
      }
    }
  },
  data() {
    return {
      eOptions: []
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
    currentPlaceholder() {
      if(this.data) {
        return ''
      } else {
        return '请选择'
      }
    }
  },
  mounted() {
    this.eOptions = list.filter(item => {
      return this.options.includes(item.value) 
    })
  },
  methods: {
    appendEmoji(item) {
      this.visible = false
      this.value = this.value + `[${item.value}]`
    }
  }
}
</script>

<style lang="scss" scoped>
.el-emoji-select {
  position: relative;
  .el-emoji-warp {
    margin: auto 21px;
  }
}
.el-emoji-item {
  width: 20px;
  height: 20px;
  padding-right: 2px;
  transform: translateY(2px);
}
</style>