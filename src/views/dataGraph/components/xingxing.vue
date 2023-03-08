<template>
  <div class="xingxing">
    <div v-for="i in num" :key="i.val" class="xx_div">
      <el-rate v-model="i.val" disabled text-color="#ff9900"> </el-rate>
      <span> {{ i.val }}星评价 </span>
      <span>2000</span>
      <span>20%</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataGraph",
  props: ["title", "isBg", "isTjy", "isJflx"],
  data() {
    return {
      num: [{ val: 5 }, { val: 4 }, { val: 3 }, { val: 2 }, { val: 1 }],
    };
  },
  created() {},
  methods: {},
};
</script>
<style lang="scss" scoped>
.xingxing {
  padding: 20px 20px 0 30px;
  box-sizing: border-box;
  .xx_div {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
    color: #fff;
    /deep/.el-rate {
      height: 30px;
      .el-rate__icon {
        font-size: 28px;
        margin-right: 10px;
      }
    }
  }
}
</style>
