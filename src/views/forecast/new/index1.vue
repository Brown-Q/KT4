<template>
  <div class="permissions-container">

    <el-row :gutter="20">
      <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">

      <el-card shadow="hover">
        <div slot="header">

      </div>
      <div class="lodash-content">
        <el-row :gutter="20">
          <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">
            <el-divider content-position="left"><h3>基于信息传播模型的传播预测方法</h3></el-divider>
            <el-card>
            基于信息传播模型的传播预测方法：该方法将实时状态指标、传播规律和时空特征作为先验知识输入到经典的信息传播模型，实现对特定信息传播的时空预测。
            状态指标：五阶段的演化状态（发生、扩散、爆发、震荡、回落）。传播规律：三方面的传播热度（关注度、回复数、转发数）。
            </el-card>
          </el-col>
          <el-col :xs="24" :sm="24" :md="12" :lg="12" :xl="12">
            <el-card shadow="hover">
              <div slot="header">
                <h3>传播规律图</h3>
<!--                <img src="../figure/qian.png" width="631" height="604" />-->
              </div>
              <img src="../figure/1.png" width="640" height="480" align="left" hspace="20" vspace="20">


            </el-card>
          </el-col>
          <el-col :xs="24" :sm="24" :md="12" :lg="12" :xl="12">
            <el-card shadow="hover">
              <div slot="header">
                <h3>预测结果图</h3>

              </div>
              <img src="../figure/2.png" width="640" height="480" align="left" hspace="20" vspace="20">
            </el-card>
          </el-col>

        </el-row>
      </div>
        <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">
        <el-card>
          <el-divider content-position="left"><h3>预测结果说明</h3></el-divider>

            <el-card>
              我们基于14天关于HK事件的Twitter数据集进行构建预测模型。首先对数据集进行处理和分析，得出该事件的传播规律，其三方面的传播热度如上面左图所示：
            </el-card>
            <br> <br>
            <el-card>
              我们根据14天中易感人群S(t),感染人群I(t),以及恢复人群R(t)的动态变化，拟合信息传播的SIR模型，得出的预测模型如下图所示。结果图中展示了一共30天的SIR曲线，
              分别经历了五阶段的演化状态（发生、扩散、爆发、震荡、回落）。0-3天是发生时期，4-7天是扩散，8-15天是爆发，16-20天会有震荡，20天之后就是回落。
              其中我们的14天的真实数据集处于第2天到第15天，其演化规律正好符合传播规律的热度图。
            </el-card>


          <br><br>
          </el-card>

        </el-col>
    </el-card>

      </el-col>



      <el-card shadow="hover">
<!--    <el-divider content-position="left">-->
<!--      <h3>阻断节点热度展示</h3>-->
<!--    </el-divider>-->
<!--    <br />-->

<!--      <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">-->
<!--        <el-table :data="tableData" style="width: 100%">-->
<!--          <el-table-column prop="name" label="姓名" width="180"></el-table-column>-->
<!--          <el-table-column prop="ID" label="账号" width="180"></el-table-column>-->
<!--          <el-table-column prop="day1" label="第一天热度"></el-table-column>-->
<!--          <el-table-column prop="day2" label="第二天热度"></el-table-column>-->
<!--          <el-table-column prop="day3" label="第三天热度"></el-table-column>-->
<!--          <el-table-column prop="day4" label="第四天热度"></el-table-column>-->
<!--          <el-table-column prop="day5" label="第五天热度"></el-table-column>-->
<!--          <el-table-column prop="day6" label="第六天热度"></el-table-column>-->
<!--          <el-table-column prop="day7" label="第七天热度"></el-table-column>-->
<!--          <el-table-column prop="day8" label="第八天热度"></el-table-column>-->
<!--          <el-table-column prop="day9" label="第九天热度"></el-table-column>-->
<!--          <el-table-column prop="day10" label="第十天热度"></el-table-column>-->
<!--          <el-table-column prop="day11" label="第十一天热度"></el-table-column>-->
<!--          <el-table-column prop="day12" label="第十二天热度"></el-table-column>-->
<!--          <el-table-column prop="day13" label="第十三天热度"></el-table-column>-->
<!--          <el-table-column prop="day14" label="第十四天热度"></el-table-column>-->


<!--        </el-table>-->
<!--      </el-col>-->
      </el-card>
    </el-row>
  </div>
</template>

<script>
  import { getList } from "@/api/blacklist";
  import { mapGetters } from "vuex";
  import { tokenTableName } from "@/config/settings";
  import JsonEditor from "@/components/JsonEditor";


  export default {
    name: "Permissions",
    components: {
      JsonEditor,
    },

    data() {
      return {
        YQ_data: [
          {
            variety: "数据集一",
            variety_value: "香港事件数据集-twitter",
            id:1,
          },
          {
            variety: "数据集二",
            variety_value: "香港事件数据集-微博",
            id:2,
          },

        ],
        form: {
          account: "",
        },
        tableData: [],
        res: [],
        selected:[],
        // currentsel:this.selectModel(id),
      };
    },
    computed: {
      ...mapGetters({
        username: "user/username",
        permissions: "user/permissions",
      }),
    },
    created() {
      this.fetchData();
    },
    mounted() {
      this.form.account = this.username;
    },
    methods: {

      selectModel(id) {
        let obj = {};
        obj = this.YQ_data.find((item) => {
          return item.id === id;//筛选出匹配数据
        });
      },
        handleChangePermission() {
        localStorage.setItem(
          tokenTableName,
          `${this.form.account}-accessToken`
        );
        location.reload();
      },
      fetchData() {
        getList().then(({ data }) => {
          this.tableData = data;
        });
      },

    },
  };
</script>
