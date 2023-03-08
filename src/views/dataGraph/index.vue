<template>
  <ScreenAdapter>
    <div class="dataGraph">
      <header>
        <div class="herd_bg">
          <span>数据上图</span>
        </div>
        <div class="head_left top38">
          <div
            v-for="i in tabs"
            :key="i"
            :class="selectTab == i ? 'selTab' : ''"
          >
            <div class="tab_name" @click="changeTab(i)">
              {{ i }}
            </div>
          </div>
        </div>
        <div class="head_right top38">
          <el-radio-group v-model="time">
            <el-radio-button label="本周"></el-radio-button>
            <el-radio-button label="本季"></el-radio-button>
            <el-radio-button label="本年"></el-radio-button>
          </el-radio-group>
        </div>
      </header>
      <main>
        <!-- 各类数据量 -->
        <div class="main-head">
          <div v-for="i in aNum" :key="i.tit">
            <img :src="i.url" alt="" />
            <div>
              <p>{{ i.tit }}</p>
              <p class="val">{{ i.val | num }}</p>
            </div>
          </div>
        </div>
        <div class="main-contain">
          <div class="main-left">
            <!-- 调解机构结案数TOP10 -->
            <div class="ml_top">
              <ggTitle title="调解机构结案数TOP10" isBg="yes" isTjy="yes" />
              <top10 />
            </div>
            <!-- 调解满意度 -->
            <div class="ml_btm">
              <ggTitle title="调解满意度" isBg="yes" />
              <xingxing />
            </div>
          </div>
          <div class="main-center">
            <!-- 东莞市行政区域图 -->
            <div class="mc_top">
              <ggTitle title="东莞市行政区域图" />
            </div>
            <!-- 纠纷数量 -->
            <div class="mc_btm">
              <ggTitle title="清溪镇-纠纷数量" />
            </div>
          </div>
          <div class="main-right">
            <!-- 纠纷类型趋势分析 -->
            <div class="mr_top">
              <ggTitle title="纠纷类型趋势分析" isBg="yes" isJflx="yes" />
            </div>
            <!-- 案源分析 -->
            <div class="mr_btm">
              <ggTitle title="案源分析" isBg="yes" />
            </div>
          </div>
        </div>
      </main>
      <footer>
        <div class="foot_bg"></div>
      </footer>
    </div>
  </ScreenAdapter>
</template>

<script>
import ScreenAdapter from "@/components/ScreenAdapter.vue";
import ggTitle from "./components/ggTitle";
import top10 from "./components/top10";
import xingxing from "./components/xingxing"; // 调解满意度

export default {
  name: "DataGraph",
  components: {
    ScreenAdapter,
    ggTitle,
    top10,
    xingxing,
  },
  data() {
    return {
      tabs: ["数据统计一站式", "工作管理一站式", "多元化解一站式"],
      selectTab: "数据统计一站式",
      time: "本周",
      aNum: [
        {
          url: require("@/assets/images/dataGraph/3数据-用户注册量.png"),
          tit: "用户注册量",
          val: 2323,
        },
        {
          url: require("@/assets/images/dataGraph/3数据-调解机构数.png"),
          tit: "调解机构数",
          val: 2323,
        },
        {
          url: require("@/assets/images/dataGraph/3数据-调解员数量.png"),
          tit: "调解员数量",
          val: 2323,
        },
        {
          url: require("@/assets/images/dataGraph/3数据-调解案件数.png"),
          tit: "调解案件量",
          val: 2323,
        },
        {
          url: require("@/assets/images/dataGraph/3数据-调解成功数.png"),
          tit: "调解成功数",
          val: 2323,
        },
        {
          url: require("@/assets/images/dataGraph/3数据-调解失败数.png"),
          tit: "调解失败数",
          val: 2323,
        },
        {
          url: require("@/assets/images/dataGraph/3数据-司法确认案件数.png"),
          tit: "司法确认案件数",
          val: 2323,
        },
        {
          url: require("@/assets/images/dataGraph/3数据-诉讼案件总量.png"),
          tit: "诉讼案件总量",
          val: 2323,
        },
      ],
    };
  },
  created() {
    this.selectTab = localStorage.getItem("selectTab") || this.selectTab;
  },
  methods: {
    changeTab(val) {
      this.selectTab = val;
      localStorage.setItem("selectTab", val);
    },
  },
  filters: {
    num: (val, fix = 2) => {
      if (val !== 0) {
        val = Number(val); // 字符串转为数字，目标数据为数字可不转
        val = "" + val.toFixed(2); // 保留两位小数并转为字符串
        let int = val.slice(0, fix * -1 - 1); // 获取整数
        // let ext = val.slice(fix * -1 - 1); // 获取到小数
        int = int.split("").reverse().join(""); // 翻转整数
        let temp = ""; // 临时变量
        for (let i = 0; i < int.length; i++) {
          temp += int[i];
          if ((i + 1) % 3 === 0 && i !== int.length - 1) {
            temp += ","; // 每隔3个数字拼接一个逗号
          }
        }
        temp = temp.split("").reverse().join(""); // 加完逗号之后翻转
        // temp = temp + ext; // 整数小数拼接
        return temp; // 返回
      } else {
        return val;
      }
    },
  },
};
</script>
<style lang="scss" scoped>
.dataGraph {
  width: 100%;
  height: 100%;
  position: relative;
  background: url("~@/assets/images/dataGraph/1背景.png") no-repeat top center;
  header {
    width: 100%;
    height: 140px;
    position: relative;
    .herd_bg {
      background: url("~@/assets/images/dataGraph/2头部背景图.png") no-repeat
        top center;
      width: 1920px;
      height: 131px;
      span {
        text-align: center;
        line-height: 140px;
        font-size: 54px;
        font-family: YouSheBiaoTiHei;
        color: #eff8fc;
        opacity: 0.89;
        text-shadow: 0px 4px 1px rgba(19, 80, 143, 0.66);
        // background: linear-gradient(
        //   0deg,
        //   rgba(119, 186, 255, 0.45) 0%,
        //   rgba(233, 248, 255, 0.45) 73.3154296875%,
        //   rgba(255, 255, 255, 0.45) 100%
        // );
        // -webkit-background-clip: text;
        // -webkit-text-fill-color: transparent;
        font-style: oblique;
        letter-spacing: 10px;
      }
    }
    .top38 {
      position: absolute;
      top: 38px;
      width: 532px;
      height: 70px;
      background: linear-gradient(
        0deg,
        rgba(5, 165, 242, 0.2) 0%,
        rgba(5, 165, 242, 0) 100%
      );
    }
    .head_left {
      left: 0;
      display: flex;
      padding-right: 54px;
      justify-content: space-around;
      align-items: center;
      box-sizing: border-box;
      font-weight: bold;
      > div {
        width: 138px;
        height: 38px;
        line-height: 38px;
        text-align: center;
        cursor: pointer;
        color: #98a5b3;
        background: url("~@/assets/images/dataGraph/1未选中.png") no-repeat top
          center;
        .tab_name {
          text-shadow: 0px 2px 8px rgba(5, 28, 55, 0.42);
        }
      }
      .selTab {
        color: #fff;
        background: url("~@/assets/images/dataGraph/2头部-选中标题.png")
          no-repeat top center;
        // color: red;
      }
    }
    .head_right {
      right: 0;
      line-height: 70px;
      text-align: right;
      padding-right: 20px;
      box-sizing: border-box;
      /deep/.el-radio-group {
        .el-radio-button__inner {
          color: #fff;
          // border: none;
          background: #011534;
          border-color: #0b3063;
        }
        .is-active {
          .el-radio-button__inner {
            background: rgba(26, 114, 225, 0.1);
            border-color: #1a72e1;
            // border: 1px solid;
            // border-image: linear-gradient(131deg, #1a72e1, #68aaff, #1a72e1) 10
            // 10;
          }
        }
      }
    }
  }
  main {
    .main-head {
      display: flex;
      padding: 0 40px;
      justify-content: space-between;
      margin-bottom: 24px;
      > div {
        display: flex;
        padding-left: 16px;
        box-sizing: border-box;
        width: 212px;
        height: 82px;
        // justify-content: space-between;
        align-items: center;
        background: url("~@/assets/images/dataGraph/3数据-边框.png") no-repeat
          top center;
        text-align: left;
        color: #fff;
        p {
          margin: 0;
        }
        img {
          margin-right: 16px;
        }
        .val {
          font-size: 24px;
          font-family: PangMenZhengDao;
          color: #3cfdff;
        }
      }
    }
    .main-contain {
      padding: 0 40px;
      box-sizing: border-box;
      display: flex;
      .main-left {
        width: 404px;
        margin-right: 80px;
        .ml_top {
          // height: 520px;
        }
      }
      .main-center {
        width: 880px;
        margin-right: 74px;
        .mc_top {
          width: 100%;
          height: 500px;
        }
      }
      .main-right {
        .mr_top {
          width: 100%;
          height: 400px;
        }
      }
    }
  }
  footer {
    position: absolute;
    padding-left: 72px;
    bottom: 0;
    .foot_bg {
      background: url("~@/assets/images/dataGraph/1底部.png") no-repeat top
        center;
      width: 1778px;
      height: 60px;
    }
  }
}
</style>
