<template>
  <div>
    <el-form ref="form" :model="form" :rules="rules" label-width="120px">
      <el-form-item label-width="0">
        <el-alert show-icon>
          策略配置
        </el-alert>
      </el-form-item>
      <el-card shadow="hover">
        <div slot="header">
          数据集选择:
          <el-select v-model="YQ_data.variety" placeholder="请选择数据集" @change="aa1">
            <el-option v-for="item in YQ_data"
                       :key="item.variety"
                       :label="item.variety_value"
                       :value="item.id"></el-option>
          </el-select>
        </div>
        <div class="lodash-content">
          <span v-if ="YQ_data.variety==1">
            <h3>数据集介绍</h3>
            twitter是一个具有发送电子邮件功能的社交新闻网站。twitter的公开数据集包含了用户发布的信息内容还有用户间的转发、评论等行为数据。
            Twitter的原始数据集也是个稀疏网络，我们剔除网络中的不活跃用户，保留参与程度高的用户。处理好的网络数据集中共包含3298个节点，
            46747 条连边，节点表示twitter用户，连边表示转发、评论等关系。
            <div class="lodash-content">
              <h3>应用场景描述</h3>
              自2019年6月以来，香港反对派和一些激进势力借和平游行集会之名，进行各种激进抗争活动。虽然特区政府已多次表示修订《逃犯条例》工作已彻底停止，
              但他们继续以“反修例”为幌子，得寸进尺、变本加厉，暴力行为不断升级，社会波及面越来越广。从6月开始的游行屡屡演变为暴力冲突，其行动完全超出了和平游行示威的范畴。
              激进分子有组织袭击警察事件开始发生，警察总部两度被包围，政府部门受到滋扰，特区立法会大楼更遭到严重冲击和大肆破坏。
            </div>
          </span>
          <span v-else>
            <h3>数据集介绍</h3>
            微博数据集包含了用户的个人信息和用户间的转发、评论等行为数据，这些数据被广泛用于研究机器学习方法和社会关系研究。微博的原始数据集是 个稀疏网络，
            我们剔除网络中的不活跃用户，保留参与程度高的用户。处理好的网络数据集中共包含4983个节点，24935条连边，节点表示微博用户， 连边表示转发、评论等关系。
            <div class="lodash-content">
              <h3>应用场景描述</h3>
              自2019年6月以来，香港反对派和一些激进势力借和平游行集会之名，进行各种激进抗争活动。虽然特区政府已多次表示修订《逃犯条例》工作已彻底停止，
              但他们继续以“反修例”为幌子，得寸进尺、变本加厉，暴力行为不断升级，社会波及面越来越广。从6月开始的游行屡屡演变为暴力冲突，其行动完全超出了和平游行示威的范畴。
              激进分子有组织袭击警察事件开始发生，警察总部两度被包围，政府部门受到滋扰，特区立法会大楼更遭到严重冲击和大肆破坏。
            </div>
          </span>
          <img src="../figure/shujuji.jpg" width="731" height="602" />
        </div>

      </el-card>
      <el-card shadow="hover">
        <div slot="header">
          引导程度选择:
          <el-select v-model="YQ_level.variety" placeholder="请选择引导程度" @change="aa2">
            <el-option v-for="item in YQ_level"
                       :key="item.variety"
                       :label="item.variety_value"
                       :value="item.id"></el-option>
          </el-select>
        </div>
        <div class="lodash-content">
          <h3>引导程度</h3>
          <span v-if ="YQ_level.variety==1">
            级别一：引导
          </span>
          <span v-else-if="YQ_level.variety==2">
            级别二：控制
          </span>
          <span v-else>
            级别三：消除
          </span>

        </div>

      </el-card>

    </el-form>
    <div class="pay-button-group">
      <el-button @click="handlePrev">上一步</el-button>
      <el-button type="primary" :loading="loading" @click="handleSubmit">
        完成
      </el-button>

    </div>
  </div>
</template>
<script>
  export default {
    props: {
      infoData: {
        type: Object,
        default: () => {
          return {};
        },
      },
    },
    data() {
      return {

        YQ_data: [
          {
            variety: "事件一",
            variety_value: "HK事件数据集-twitter",
            id:1,
          },
          {
            variety: "事件二",
            variety_value: "HK事件数据集-微博",
            id:2,
          },

        ],
        YQ_level: [
          {
            variety: "等级一",
            variety_value: "等级一",
            id:1,
          },
          {
            variety: "等级二",
            variety_value: "等级二",
            id:2,
          },
          {
            variety: "等级三",
            variety_value: "等级三",
            id:3,
          },

        ],
        form: {
          password: "",
        },
        rules: {
          password: [
            { required: true, message: "请输入支付密码", trigger: "blur" },
          ],
        },
        loading: false,
      };
    },
    methods: {

      handleSubmit() {
        this.$refs.form.validate((valid) => {
          if (valid) {
            this.loading = true;
            setTimeout(() => {
              this.$emit("change-step", 3);
              this.loading = false;
            }, 20);
          } else {
            this.loading = false;
          }
        });
      },
      aa1(id, type){
        this.infoData.gatheringAccount=id
        return id;
      },
      aa2(id, type){
        this.infoData.gatheringName=id
        return id;
      },

      handlePrev() {
        this.$emit("change-step", 1);
      },
    },
  };
</script>
<style lang="scss" scoped>
  .pay-button-group {
    display: block;
    margin: 20px auto;
    text-align: center;
  }
</style>
