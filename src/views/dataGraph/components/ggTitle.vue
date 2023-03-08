<template>
  <div class="ggTitle" :class="isBg ? 'bgUrl' : ''">
    <!-- 标题 -->
    <span class="tit">
      {{ title || "调解机构结案数TOP10" }}
    </span>
    <!-- 调解员结案数 -->
    <div class="sel tjyjas" v-if="isTjy">
      <el-select v-model="tjy" size="small" placeholder="请选择">
        <el-option
          v-for="item in options1"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        >
        </el-option>
      </el-select>
    </div>
    <!-- 纠纷类型 -->
    <div class="sel jflx" v-if="isJflx">
      <span class="lable-name">纠纷类型</span>
      <el-select v-model="jflx" size="small" placeholder="请选择">
        <el-option
          v-for="item in options1"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        >
        </el-option>
      </el-select>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataGraph",
  props: ["title", "isBg", "isTjy", "isJflx"],
  data() {
    return {
      options1: [
        {
          value: "选项1",
          label: "黄金糕",
        },
        {
          value: "选项2",
          label: "双皮奶",
        },
        {
          value: "选项3",
          label: "蚵仔煎",
        },
        {
          value: "选项4",
          label: "龙须面",
        },
        {
          value: "选项5",
          label: "调解机构结案数",
        },
      ],
      tjy: "调解机构结案数",
      jflx: "全部",
    };
  },
  created() {},
  methods: {},
};
</script>
<style lang="scss" scoped>
.ggTitle {
  width: 404px;
  height: 30px;
  text-align: left;
  padding-left: 45px;
  box-sizing: border-box;
  position: relative;
  .tit {
    font-size: 20px;
    font-family: Source Han Sans CN;
    font-weight: bold;
    font-style: italic;
    color: #ffffff;
    position: relative;
    top: -10px;
    // background: linear-gradient(
    //   0deg,
    //   rgba(14, 197, 236, 0.36) 0%,
    //   rgba(49, 190, 255, 0.36) 0%,
    //   rgba(239, 252, 254, 0.36) 58.7646484375%
    // );
    // -webkit-background-clip: text;
    // -webkit-text-fill-color: transparent;
  }
  .sel {
    position: absolute;
    right: 0;
    top: -10px;
    .lable-name {
      color: #fff;
      margin-right: 6px;
    }
    /deep/.el-select {
      width: 116px;
      .el-input__inner {
        // padding: 0 10px;
        background: rgba(26, 114, 225, 0.1);
        border: 1px solid;
        // border-image: linear-gradient(131deg, #1a72e1, #68aaff, #1a72e1) 10 10;
        border-color: #1a72e1;
        border-radius: 4px;
        // font-size: 14px;
        font-family: Source Han Sans CN;
        font-weight: bold;
        color: #ffffff;
        padding-left: 8px;
        box-sizing: border-box;
        // border-radius: 8px;
        // overflow: hidden;
        // text-overflow: ellipsis;
        // white-space: nowrap;
      }
      .el-input__inner::-webkit-input-placeholder {
        color: #fff !important;
      }
    }
  }
}
.bgUrl {
  background: url("~@/assets/images/dataGraph/4TOP10-标题背景.png") no-repeat
    top center;
}
</style>
