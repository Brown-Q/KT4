<template>
  <div>
    <div class="pay-top-content">
      <vab-icon class="pay-success" :icon="['fas', 'check-circle']"></vab-icon>
      <p>策略选择及配置完成</p>
    </div>
    <el-form
      ref="form"
      :model="form"
      :rules="rules"
      label-width="120px"
      class="pay-bottom"
    >
      <el-form-item label="选择的策略：">

        <span  v-if ="infoData.payAccount==1" >
            基于竞争的传播引导策略
          </span>
        <span v-else-if="infoData.payAccount==2">
            基于结构化阻断的引导策略
          </span>
        <span v-else>
            基于社区阻断的引导策略
          </span>

      </el-form-item>
      <el-form-item label="选择的数据集：">
<!--        {{ infoData.gatheringAccount }}-->
        <span v-if ="infoData.gatheringAccount==1">
          HK事件数据集-twitter
        </span>
        <span v-else>
          HK事件数据集-微博
        </span>

      </el-form-item>
      <el-form-item label="引导级别：">
<!--        {{ infoData.gatheringName }}-->
        <span v-if ="infoData.gatheringName==1">
            级别一：引导
          </span>
        <span v-else-if="infoData.gatheringName==2">
            级别二：控制
          </span>
        <span v-else>
            级别三：消除
          </span>
      </el-form-item>

    </el-form>
    <div class="pay-button-group">
      <el-button type="primary" @click="handlePrev">重新选择策略</el-button>
      <el-button type="link" @click="handle">引导效果展示</el-button>
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
        form: {
          password: "123456",
        },
        rules: {
          password: [
            { required: true, message: "请输入支付密码", trigger: "blur" },
          ],
        },
        loading: false,
      };
      var a = sessionStorage.getItem('cl')
    },
    created(){
      this.getinfo();
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
      getinfo(){
        var sel1=this.$route.params.num;
        return sel1;
      },
      handlePrev() {
        this.$emit("change-step", 1);
      },
      handle(){
        this.$router.push({name:'GoodsList'})
      },
    },
  };
</script>
<style lang="scss" scoped>
  .pay-top-content {
    text-align: center;

    .pay-success {
      display: block;
      margin: 20px auto 5px auto;
      font-size: 40px;
      color: $base-color-green;
    }
  }

  .pay-bottom {
    padding: 20px;
    margin-top: 20px;
    background: #f5f7f8;
    border: 1px dashed $base-color-gray;
  }

  .pay-button-group {
    display: block;
    margin: 20px auto;
    text-align: center;
  }
</style>
