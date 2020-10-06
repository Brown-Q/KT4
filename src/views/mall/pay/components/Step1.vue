<template>
  <div>
    <el-form ref="form" :model="form" :rules="rules" label-width="120px">
      <el-form-item label-width="0">
        <el-alert show-icon>请从策略库中选择策略</el-alert>
      </el-form-item>
      <el-card shadow="hover">
        <div slot="header">
          选择策略：
            <el-select id="select1" v-model="strategy.variety" placeholder="请选择策略" @change="aa">
          <el-option v-for="item in strategy"
                     :key="item.variety"
                     :label="item.variety_value"
                     :value="item.id"></el-option>
        </el-select>
        </div>
        <div class="lodash-content">
          <h3>策略描述</h3>
          <span  v-if ="strategy.variety==1" >
            基于竞争的传播引导策略
          </span>
          <span v-else>
            基于结构阻断的YQ引导策略技术提供了一种在社交网络中封锁YQ社区并抑制YQ传播的方法。采用局部节点或边的阻断方法，解决单一传播环境下最小代价YQ社区封锁优化问题。
            利用基于最小顶点覆盖的贪婪(MVCBG) 算法来寻找合适的节点进行封锁，阻断YQ事件进一步扩散。
          </span>


        </div>
      </el-card>

    </el-form>
    <div class="pay-button-group">
      <el-button type="primary" @click="handleSubmit">下一步</el-button>
    </div>
  </div>
</template>
<script>

  // function aa(id, type) {
  //   var inner = document.getElementById('select1').innerHTML;
  //   // var index1=inner.selectIndex
  //   alert(inner)
  //   return id
  // }
  export default {
    data() {
      // var a=this.methods.aa();

      return {
        form: {
          payAccount: "",
          gatheringAccount: "1204505",
          gatheringName: "123",
          price: "100",
        },
        strategy: [
          {
            variety: "第一个",
            variety_value: "基于竞争的传播引导策略",
            id:1,
          },
          {
            variety: "第二个",
            variety_value: "基于结构化阻断的引导策略",
            id:2,
          },


        ],
        rules: {
          // payAccount: [
          //   { required: true, message: "请选择付款账户", trigger: "blur" },
          // ],
          // gatheringAccount: [
          //   { required: true, message: "请输入收款账户", trigger: "blur" },
          //   { type: "email", message: "账户名应为邮箱格式", trigger: "blur" },
          // ],
          // gatheringName: [
          //   { required: true, message: "请输入收款人姓名", trigger: "blur" },
          // ],
          // price: [
          //   { required: true, message: "请输入转账金额", trigger: "blur" },
          //   { pattern: /^(\d+)((?:\.\d+)?)$/, message: "请输入合法金额数字" },
          // ],
        },
      };
    },
    created(){
    },
    methods: {
      // get(){
      //   var b=this.aa(1,'sss');
      //   alert(b)
      // },

      handleSubmit() {
        this.$refs.form.validate((valid) => {
          if (valid) {
            this.$emit("change-step", 2, this.form);
          }
        });
      },
      aa(id, type){
        this.form.payAccount=id
        return id;
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
