<template>
  <div class="permissions-container">

    <el-row :gutter="20">
      <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12">

      <el-card shadow="hover">
        <div slot="header">
          数据集选择:
          <el-select id="select1" v-model="YQ_data.variety"  name="s1" placeholder="香港事件数据集-微博" >
            <el-option v-for="item in YQ_data"
                       :key="item.variety"
                       :label="item.variety_value"
                       :value="item.id"></el-option>
          </el-select>
      </div>
      <div class="lodash-content">


        <h3>事件描述</h3>

        香港“占中”事件在社交网络上引起了广泛的讨论，境外媒体和记者在社交网路上发布一些内容抹黑香港警察，用一些夸张虚假的内容引导群众舆论，因此对舆论进行正确的引导是必须的。
        <br>
        <h3>数据集描述</h3>
        <span v-if ="YQ_data.variety==1">
          twitter是一个具有发送电子邮件功能的社交新闻网站。twitter的公开数据集包含了用户发布的信息内容还有用户间的转发、评论等行为数据。
          Twitter的原始数据集也是个稀疏网络，我们剔除网络中的不活跃用户，保留参与程度高的用户。处理好的网络数据集中共包含3298个节点，46747
          条连边，节点表示twitter用户，连边表示转发、评论等关系。1）重要节点发现的准确率
        </span>
        <span v-else>
          微博数据集包含了用户的个人信息和用户间的转发、评论等行为数据，这些数据被广泛用于研究机器学习方法和社会关系研究。微博的原始数据集是
          个稀疏网络，我们剔除网络中的不活跃用户，保留参与程度高的用户。处理好的网络数据集中共包含4983个节点，24935条连边，节点表示微博用户，
          连边表示转发、评论等关系。
        </span>
      </div>

    </el-card>
      </el-col>


      <el-card shadow="hover">
    <el-divider content-position="left">
      特征展示
    </el-divider>
    <br />

      <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">
        <el-table :data="tableData" style="width: 100%">
          <el-table-column prop="name" label="名称" width="180"></el-table-column>
          <el-table-column prop="ID" label="标签号" width="180"></el-table-column>
          <el-table-column prop="category" label="类别"></el-table-column>
        </el-table>
      </el-col>
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
