<template>
  <div class="top10">
    <div v-for="(i, index) in top10Data" :key="index" class="top_div">
      <img :src="imgUrl" alt="" class="sanjiao" />
      <span class="xuhao">
        <img v-if="index == 0" :src="xh1" alt="" />
        <img v-else-if="index == 1" :src="xh2" alt="" />
        <img v-else-if="index == 2" :src="xh3" alt="" />
        <span v-else>
          {{ index + 1 }}
        </span>
      </span>
      <el-tooltip
        class="item"
        effect="dark"
        content="机构12倒计时能看到你上课呢"
        placement="right"
      >
        <span class="jg"> {{ i.name }} </span>
      </el-tooltip>
      <span>
        <span
          v-if="index == 0"
          class="line l1"
          :style="{ width: i.val ? `148px` : '0' }"
        ></span>
        <span
          v-else-if="index == 1"
          class="line l2"
          :style="{
            width: i.val
              ? `${(i.val / top10Data[index - 1].val) * 148}px`
              : '0',
          }"
        ></span>
        <span
          v-else-if="index == 2"
          class="line l3"
          :style="{
            width: i.val
              ? `${(i.val / top10Data[index - 1].val) * 148}px`
              : '0',
          }"
        ></span>
        <span
          v-else
          class="line"
          :style="{
            width: i.val
              ? `${(i.val / top10Data[index - 1].val) * 148}px`
              : '0',
          }"
        ></span>
      </span>
      <span class="val">{{ i.val }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataGraph",
  props: [],
  data() {
    return {
      imgUrl: require("@/assets/images/dataGraph/4TOP10-三角.png"),
      xh1: require("@/assets/images/dataGraph/4TOP10-1.png"),
      xh2: require("@/assets/images/dataGraph/4TOP10-2.png"),
      xh3: require("@/assets/images/dataGraph/4TOP10-3.png"),
      flag: false,
      top10Data: [
        {
          name: "机构1111111111111",
          val: 2060,
        },
        {
          name: "机构1111111111111",
          val: 1900,
        },
        {
          name: "机构1111111111111",
          val: 1700,
        },
        {
          name: "机构1111111111111",
          val: 1500,
        },
        {
          name: "机构1111111111111",
          val: 1300,
        },
        {
          name: "机构1111111111111",
          val: 1100,
        },
        {
          name: "机构1111111111111",
          val: 900,
        },
        {
          name: "机构1111111111111",
          val: 700,
        },
        {
          name: "机构1111111111111",
          val: 500,
        },
        {
          name: "机构1111111111111",
          val: 300,
        },
      ],
    };
  },
  created() {},
  methods: {},
};
</script>
<style lang="scss" scoped>
.top10 {
  width: 100%;
  .top_div {
    width: 100%;
    display: flex;
    height: 34px;
    background: linear-gradient(90deg, #00295b 0%, rgba(27, 114, 222, 0) 100%);
    margin: 16px 0;
    position: relative;
    padding: 0 12px 0 25px;
    box-sizing: border-box;
    align-items: center;
    box-sizing: border-box;
    .sanjiao {
      width: 4px;
      height: 4px;
      position: absolute;
      top: 5px;
      left: 5px;
    }
    .xuhao {
      color: #fff;
      font-size: 18px;
      display: inline-block;
      width: 30px;
      img {
        width: 22px;
        height: 24px;
        display: inline-block;
      }
    }
    .jg {
      font-size: 16px;
      color: #fff;
      margin-left: 20px;
      width: 80px;
      overflow: hidden;
      white-space: nowrap;
      text-overflow: ellipsis;
    }
    .line {
      display: inline-block;
      width: 148px;
      height: 8px;
      background: linear-gradient(
        90deg,
        rgba(103, 203, 255, 0) 0%,
        #67cbff 100%
      );
      border-radius: 4px;
      margin-left: 10px;
    }
    .l1 {
      background: linear-gradient(90deg, rgba(255, 222, 0, 0) 0%, #ffde00 100%);
    }
    .l2 {
      background: linear-gradient(
        90deg,
        rgba(103, 249, 180, 0) 0%,
        #67f9b4 100%
      );
    }
    .l3 {
      background: linear-gradient(90deg, rgba(0, 186, 255, 0) 0%, #00baff 100%);
    }
    .val {
      font-size: 18px;
      font-family: D-DIN;
      font-weight: bold;
      font-style: italic;
      color: #67cbff;
      line-height: 48px;
      opacity: 0.8;
      position: absolute;
      right: 12px;
    }
  }
}
</style>
