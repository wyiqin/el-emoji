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
      contentStr: ""
    };
  },
  created() {},
  methods: {
    format(arr = []) {
      console.log("start", this.contentStr, arr);
      if (this.contentStr[0] !== "[") {
        let index = this.contentStr.indexOf("[");
        arr.push(this.contentStr.slice(0, index));
        this.contentStr = this.contentStr.slice(index);
      } else {
        let index = this.contentStr.indexOf("]");
        if (index === -1) {
          arr.push(this.contentStr);
          this.contentStr = "";
        } else {
          this.contentStr = this.contentStr.replace( /^\[(.+)\]/, (res, res1) => {
            console.log(res,res1,'正则');
            
              let item = list.find(item => item.value === res1);
              console.log(item, "find");
              if (item) {
                arr.push(
                  <img class="el-emoji-item" src={item.img} alt={item.value} />
                );
              } else {
                arr.push(res);
              }

              return "";
            }
          );
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
    content: {
      handler() {
        this.contentStr = this.content;
        this.domArr = this.format();
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
  transform: translateY(2px);
}
</style>