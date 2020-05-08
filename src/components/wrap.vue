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
  name: "ElEmojiWrap",
  props: {
    content: {
      type: String,
      default() {
        return "[哈哈]你好饿了么";
      }
    }
  },
  data() {
    return {
    };
  },
  created() {},
  methods: {
    format(arr = []) {
      if (this.contentStr[0] !== "[") {
        let index = this.contentStr.indexOf("[");
        if(index === -1) {
          arr.push(this.contentStr);
          this.contentStr = ''
        } else {
          arr.push(this.contentStr.slice(0, index));
          this.contentStr = this.contentStr.slice(index);
        }
      } else {
        let index = this.contentStr.indexOf("]");
        if (index === -1) {
          arr.push(this.contentStr);
          this.contentStr = "";
        } else {
          let index = this.contentStr.indexOf(']')
          if(index === -1) {
            arr.push(this.contentStr)
            this.contentStr = ''
          } else {
            let emojiName = this.contentStr.slice(1,index)
            this.contentStr = this.contentStr.slice(index+1)
            let item = list.find(item => item.value === emojiName);
              if (item) {
                arr.push(
                  <img class="el-emoji-item" src={item.img} alt={item.value} />
                );
              } else {
                arr.push(`[${emojiName}]`);
              }
          }
        }
      }
      if (this.contentStr) {
        return this.format(arr);
      } else {
        return arr;
      }
    }
  },
  watch: {
    content: { // 防抖优化
      handler(val) {
        this.contentStr = val;
        this.domArr = this.format();
        this.$forceUpdate()
      },
      immediate: true
    }
  },
  render() {
    return <span>{...this.domArr}</span>;
  }
};
</script>

<style scoped>
.el-emoji-item {
  width: 20px;
  height: 20px;
  padding-right: 2px;
  transform: translateY(2px);
}
</style>