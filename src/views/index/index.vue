<template>
  <div class="index-container">
    <el-row :gutter="20">
      <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">
        <el-alert
          v-if="noticeList[0]"
          :title="noticeList[0].title"
          :closable="noticeList[0].closable"
        >
        </el-alert>
      </el-col>
      <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">
        <el-card shadow="never">
          <center><h2>课题4引导效果展示平台总体功能</h2></center>
        </el-card>
      </el-col>
      <el-col :xs="24" :sm="24" :md="8" :lg="8" :xl="8">
        <el-card shadow="never">
          <div slot="header">
            <el-button style="font-size: 16px; font-weight: bold" type="link" @click="handle">舆情态势评估和引导策略</el-button>
            <br><br>
<!--            <h3>舆情态势评估和引导策略</h3>-->
            <span>
              研究舆情信息传播时空预测模型，研究揭示特定信息在不同网络通道中传播的时间、空间规律。挖掘影响舆情信息传播的微观特征和宏观要素，
              研究建立信息传播能力的计算方法。结合特定信息传播的实时状态指标、传播规律和时空特征，研究敏感舆情舆情宏观态势的量化测度、特定信
              息传播的实时预测算法和空间维预测算法和实时在线化处理方法。首先从情感、行为、认知和传播态势四个方面对事件进行评分，然后根据事件
              的态势评分对事件进行评级，最后根据舆情事件的等级，分别从技术引导策略库和心理引导策略库选取合适的策略进行组合引导。
            </span>
            <br><br>
            <img src="../figure/yindao1.jpg" width="480" height="300" @click="handle"/>
          </div>
        </el-card>
      </el-col>
      <el-col :xs="24" :sm="24" :md="8" :lg="8" :xl="8">
        <el-card shadow="never">
          <div slot="header">
            <el-button style="font-size: 16px; font-weight: bold" type="link" @click="handle2">意见领袖发现与跟踪</el-button>
            <br><br>
            <span>
              研究综合考虑用户间影响力和同质性、消息发表时序等因素对信息传播的影响。研究网络个体影响力评价技术，分析其在话题观点形成和舆论传播过程
              中所起的作用，进而为实现舆情引导虚拟人的自动培育提供理论指导。研究基于用户指纹的意见领袖行为分析与跟踪技术。通过综合分析用户的属性特
              征及行为特征，以及分析用户在网络中的结构特征构成用户指纹特征，建立高维度节点身份映射模型，对跨网络的不同用户进行身份对齐，从而实现对目标节点不同账号的跟踪。
              <br><br><br>
            </span>
            <img src="../figure/yindao2.jpg" width="480" height="300" @click="handle2"/>

          </div>
        </el-card>
      </el-col>
      <el-col :xs="24" :sm="24" :md="8" :lg="8" :xl="8">
        <el-card shadow="never">
          <div slot="header">
            <el-button style="font-size: 16px; font-weight: bold" type="link" @click="handle3">引导策略工具库和效果展示</el-button>
            <br><br>
<!--            <h3>引导策略工具库和效果展示</h3>-->
            <span>
              研究适应性不同事件性质和引导目的的弹性引导策略。研究基于竞争性传播模型的热度削减技术，抑制特定事件的关注度，提高具有环境感知能力的多主
              体协同引导能力。研究基于正负激励与心理威慑的传播增益技术，舆情引导态势走向。研究舆情引导效果量化评估指标体系和计算方法，实现对引导和调节效果的客观评价。
              针对舆情信息对大规模突发事件和社会意识形态的影响周期，研究不同阶段舆情信息干预效果评估机制。
              <br><br>
            </span>
            <br><br>
            <img src="../figure/yindao3.jpg" width="480" height="300" @click="handle3" />
          </div>
        </el-card>
      </el-col>





    </el-row>
  </div>
</template>

<script>
  import VabChart from "@/plugins/echarts";
  import { dependencies, devDependencies } from "../../../package.json";
  import { getList } from "@/api/changeLog";
  import { getNoticeList } from "@/api/notice";
  import { getRepos, getStargazers } from "@/api/github";
  export default {
    name: "Index",
    components: {
      VabChart,
    },
    data() {
      return {
        timer: 0,
        updateTime: process.env.VUE_APP_UPDATE_TIME,
        nodeEnv: process.env.NODE_ENV,
        dependencies: dependencies,
        devDependencies: devDependencies,
        config1: {
          startVal: 0,
          endVal: this.$baseLodash.random(20000, 60000),
          decimals: 0,
          prefix: "",
          suffix: "",
          separator: ",",
          duration: 8000,
        },
        config2: {
          startVal: 0,
          endVal: this.$baseLodash.random(1000, 20000),
          decimals: 0,
          prefix: "",
          suffix: "",
          separator: ",",
          duration: 8000,
        },
        config3: {
          startVal: 0,
          endVal: this.$baseLodash.random(1000, 20000),
          decimals: 0,
          prefix: "",
          suffix: "",
          separator: ",",
          duration: 8000,
        },

        //访问量

        //授权数

        //词云

        //中国地图


        //更新日志
        reverse: true,
        activities: [],
        noticeList: [],
        //其他信息
        userAgent: navigator.userAgent,
        //卡片图标

      };
    },
    created() {
      this.fetchData();
    },
    beforeDestroy() {
      clearInterval(this.timer);
    },

    methods: {
      handle(){
        this.$router.push({name:'UserManagement'})
      },
      handle2(){
        this.$router.push({name:'Permission'})
      },
      handle3(){
        this.$router.push({name:'Pay'})
      },
      handleClick(e) {
        this.$baseMessage(`点击了${e.name},这里可以写跳转`);
      },
      handleZrClick(e) {},
      handleChangeTheme() {
        this.$baseEventBus.$emit("theme");
      },
      async fetchData() {
        const { data } = await getList();
        data.map((item, index) => {
          if (index === data.length - 1) {
            item.color = "#0bbd87";
          }
        });
        this.activities = data;
        const res = await getNoticeList();
        this.noticeList = res.data;
        /* getRepos({
        token: "1061286824f978ea3cf98b7b8ea26fe27ba7cea1",
      }).then((res) => {
        const per_page = Math.ceil(res.data.stargazers_count / 100);
        alert(per_page);
        getStargazers({
          token: "1061286824f978ea3cf98b7b8ea26fe27ba7cea1",
          page: 1,
          per_page: res.per_page,
        }).then((res) => {
          alert(JSON.stringify(res));
        });
      }); */
      },
    },
  };
</script>

<style lang="scss" scoped>
  .index-container {
    padding: 0 !important;
    margin: 0 !important;
    background: #f5f7f8 !important;

    ::v-deep {
      .el-alert {
        padding: $base-padding;

        &--info.is-light {
          min-height: 82px;
          padding: $base-padding;
          margin-bottom: 15px;
          color: #909399;
          background-color: $base-color-white;
          border: 1px solid #ebeef5;
        }
      }

      .el-card__body {
        .echarts {
          width: 100%;
          height: 125px;
        }
      }
    }

    .card {
      min-height: 400px;

      ::v-deep {
        .el-card__body {
          .echarts {
            width: 100%;
            height: 305px;
          }
        }
      }
    }

    .bottom {
      padding-top: 20px;
      margin-top: 5px;
      color: #595959;
      text-align: left;
      border-top: 1px solid $base-border-color;
    }

    .table {
      width: 100%;
      color: #666;
      border-collapse: collapse;
      background-color: #fff;

      td {
        position: relative;
        min-height: 20px;
        padding: 9px 15px;
        font-size: 14px;
        line-height: 20px;
        border: 1px solid #e6e6e6;

        &:nth-child(odd) {
          width: 20%;
          text-align: right;
          background-color: #f7f7f7;
        }
      }
    }

    .icon-panel {
      height: 100px;
      text-align: center;
      cursor: pointer;

      svg {
        font-size: 40px;
      }

      p {
        margin-top: 10px;
      }
    }

    .bottom-btn {
      button {
        margin: 5px 10px 15px 0;
      }
    }
  }
</style>
