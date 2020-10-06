<template>
  <div class="tree-container">
    <el-row :gutter="20">
      <el-col :xs="6" :sm="6" :md="6" :lg="6" :xl="6">
        <el-divider content-position="left"><h3>YQ事件选择</h3></el-divider>
        <el-input v-model="filterText" placeholder="输入关键字查询" />
        <el-tree
          ref="demoTree"
          :data="data2"
          :default-checked-keys="defaultCheckedKeys"
          :default-expanded-keys="defaultExpendedKeys"
          :expand-on-click-node="false"
          :filter-node-method="filterNode"
          :highlight-current="true"
          :props="defaultProps"
          class="vab-filter-tree"
          node-key="id"
          @check="checkNode"
          @node-click="nodeClick"
          @node-collapse="nodeCollapse"
          @node-expand="nodeExpand"
        >

        </el-tree>
      </el-col>
<!--      <el-col :xs="24" :sm="24" :md="8" :lg="8" :xl="8">-->
<!--        <el-card shadow="never">-->
<!--          <div slot="header">-->
<!--            <h3>舆情态势评估和引导策略</h3>-->
<!--            <span>-->
<!--              舆情态势评估和引导策略舆情态势评估和引导策略舆情态势评估和引导策略舆情态势评估和引导策略舆情态势评估和引导策略舆情态势评估和引导策略舆情态势评估和引导策略-->
<!--            </span>-->
<!--            <br><br>-->
<!--            <img src="../figure/yindao1.jpg" width="420" height="300" />-->
<!--          </div>-->
<!--        </el-card>-->
<!--      </el-col>-->
      <el-col :xs="18" :sm="18" :md="18" :lg="18" :xl="18">
        <el-divider content-position="left"><h3>YQ事件相关信息</h3></el-divider>
          <el-card shadow="never">
            <div slot="header">
              <h3>香港事件</h3>
              <span>
                自2019年6月以来，香港反对派和一些激进势力借和平游行集会之名，进行各种激进抗争活动。虽然特区政府已多次表示修订《逃犯条例》工作已彻底停止，
                但他们继续以“反修例”为幌子，得寸进尺、变本加厉，暴力行为不断升级，社会波及面越来越广。从6月开始的游行屡屡演变为暴力冲突，其行动完全超出了和平游行示威的范畴。
                激进分子有组织袭击警察事件开始发生，警察总部两度被包围，政府部门受到滋扰，特区立法会大楼更遭到严重冲击和大肆破坏。
              </span>
              <br><br>
              <img src="../figure/HKzhanzhong.jpg" width="1130" height="300" />
            </div>
          </el-card>

      </el-col>

      <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">
<!--        <el-divider content-position="left">YQ事件评级</el-divider>-->
        <el-card shadow="never">
          <div slot="header">

            <el-divider content-position="left">
              <h3>YQ事件态势评估</h3>
            </el-divider>
            <br>
            <img src="../figure/leida.jpg" width="700" height="830"  align="left" hspace="20" vspace="20"/>
            <h3>情感</h3>
            <h4>a）舆论内容情感倾向</h4>
            i.	正向情感词频：舆论内容中正向情感词出现的次数<br>
            ii.	负向情感词频：舆论内容中负向情感词出现的次数<br>
            <h4>b）受众评论情感倾向</h4>
            i.	正向评论占比：正向评论的数量/评论的总数量<br>
            ii.	负向评论占比：负向评论的数量/评论总数量<br>
            <h3>行为</h3>
            <h4>a）受众参与行为</h4>
            i.	受众基本信息：用于参与舆情的受众年龄、性别分布等的展示<br>
            ii.	转发量：舆论转发总数量<br>
            iii.	点赞量：舆论点赞总数量<br>
            iv.	评论量：舆论评论总数量<br>
            v.	深度转发率：带有文字的转发数量/舆论转发总数目<br>
            vi.	直接扩散率：带有@用户的评论数量/舆论评论总数目<br>
            <h4>b）博主发布行为</h4>
            i.	发布时间区间：将一天分成不同的时间段（例如每4个小时为一个时间段），用于展示舆情发布时间段的分布情况，不同的发布时间对于舆情的迅速响应具有不同的影响。<br>
            ii.	发布形式：包括文字、图片+文字、视频+文字。不同的发布形式对于舆情的传播具有不同的影响力和用户冲击力。<br>
            iii.	发布地域：用于展示发布该舆情的地域分布情况。<br>
            iv.	博主权威度：通过发布微博的博主粉丝数、博主发布微博总数、是否有微博认证、微博等级以及博文质量五项指标的加权求和来进行计算。其中博文质量涉及到博主发过的博文的转发数、评论数和赞数的加权求和。<br>
            <h4>c）受众与博主的互动行为</h4>
            i.	总互动率：博主参与回复或者点赞受众评论的总数目/评论总数目<br>
            ii.	正向互动数：博主肯定受众评论或点赞的数目<br>
            iii.	负向互动数：博主否定受众评论的数目<br>
            <h3>认知</h3>
            <h4>a）博主认知</h4>
            i.	博主是否继续发表言论<br>
            ii.	博主是否删除言论<br>
            iii.	博主是否保持沉默<br>
            <h4>b）受众认知</h4>
            i.	受众是否参与讨论：回复博主对于评论的评论即视为讨论<br>
            ii.	受众是否删除言论<br>
            iii.	受众是否保持沉默<br>

<!--            <img src="../figure/HKzhanzhong.jpg" width="1010" height="300" />-->
          </div>
        </el-card>
      </el-col>
<!--      <el-col :xs="24" :sm="24" :md="24" :lg="6" :xl="6">-->
<!--        <el-divider content-position="left">多选树</el-divider>-->
<!--        <el-select-->
<!--          v-model="multipleSelectTreeVal"-->
<!--          class="vab-tree-select"-->
<!--          clearable-->
<!--          collapse-tags-->
<!--          multiple-->
<!--          popper-class="select-tree-popper"-->
<!--          @change="changeMultipleSelectTreeHandle"-->
<!--          @clear="selectTreeClearHandle('multiple')"-->
<!--          @remove-tag="removeSelectTreeTag"-->
<!--        >-->
<!--          <el-option :value="multipleSelectTreeKey">-->
<!--            <el-tree-->
<!--              id="multipleSelectTree"-->
<!--              ref="multipleSelectTree"-->
<!--              :current-node-key="multipleSelectTreeKey"-->
<!--              :data="selectTreeData"-->
<!--              :default-checked-keys="selectTreeDefaultSelectedKeys"-->
<!--              :default-expanded-keys="selectTreeDefaultSelectedKeys"-->
<!--              :highlight-current="true"-->
<!--              :props="selectTreeDefaultProps"-->
<!--              node-key="id"-->
<!--              show-checkbox-->
<!--              @check="multipleSelectTreeCheckNode"-->
<!--            ></el-tree>-->
<!--          </el-option>-->
<!--        </el-select>-->
<!--      </el-col>-->
    </el-row>
    <!--添加/编辑节点弹框-------------------start-->
    <el-dialog
      :title="dialogTitle"
      :visible.sync="treeDialogVisible"
      class="tree-operate-dialog"
      width="400px"
      @close="treeDialogVisible = false"
    >
      <el-form ref="treeForm" :model="treeForm">
        <el-form-item label="节点名称" required>
          <el-input v-model="treeForm.name"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="treeDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="saveTree">确 定</el-button>
      </div>
    </el-dialog>
    <!--添加/编辑节点弹框-------------------end-->
  </div>
</template>

<script>
  import { getTreeList } from "@/api/tree";

  export default {
    name: "Tree",
    data() {
      return {
        dialogTitle: "添加节点",
        treeFlag: 0,
        treeDialogVisible: false,
        treeForm: {
          id: "",
          name: "",
        },
        checkNodeKeys: [],
        filterText: "",
        data2: [],
        defaultProps: {
          children: "children",
          label: "name",
        },
        defaultExpendedKeys: [],
        defaultCheckedKeys: [],
        loading: true,
        keyW: "",
        filterDevLlist: [],
        isShow: false,
        updateTree: true,
        /* 单选树-多选树---------开始 */
        selectLevel: 4, // 树可选叶子level等级
        singleSelectTreeVal: "", //单选树默认label值
        singleSelectTreeKey: "", //单选树默认key值
        selectTreeData: [], //单选树的值
        selectTreeDefaultSelectedKeys: [], //单选树默认展开的key值数组
        selectTreeDefaultProps: {
          children: "children",
          label: "name",
        },
        multipleSelectTreeVal: [], //多选树默认label值
        multipleSelectTreeKey: "", //多选树默认key值
        /* 单选树-多选树---------结束 */
      };
    },
    watch: {
      filterText(val) {
        this.$refs.demoTree.filter(val);
      },
    },
    mounted() {
      this.$nextTick(() => {
        this.getTreeListFuc(1);
        this.setCheckedKeys();

      });
    },
    methods: {
      // 树level小于n级展开方法
      openTree(treeData, n) {
        const each = (data) => {
          data.forEach((e) => {
            if (e.rank <= n) {
              this.defaultExpendedKeys.push(e.id);
            }
            if (e.children.length > 0) {
              each(e.children);
            }
          });
        };

        each(treeData);
      },
      // 获取tree数据
      async getTreeListFuc(flag) {
        const { data } = await getTreeList();
        this.data2 = data;
        if (flag) {
          this.openTree(this.data2, 2);
        }
      },
      // 节点过滤操作
      filterNode(value, data) {
        if (!value) return true;
        return data.name.indexOf(value) !== -1;
      },
      // 添加节点操作
      append(node, data, flag) {
        this.treeFlag = flag;
        this.dialogTitle = "添加节点";
        this.treeForm = {
          id: "",
          name: "",
        };
        this.treeDialogVisible = true;
      },
      // 编辑节点操作
      edit(node, data, flag) {
        this.treeFlag = flag;
        this.dialogTitle = "编辑节点";
        this.treeForm = {
          id: data.id,
          name: data.name,
        };
        this.treeDialogVisible = true;
      },
      // 删除节点操作
      remove(node, data) {
        this.$baseConfirm("你确定要删除该节点?", null, async () => {
          const { msg } = getTreeList();
          this.$baseMessage(msg, "success");
          this.getTreeListFuc(0);
        });
      },
      // 保存添加和编辑
      saveTree() {
        this.$refs.treeForm.validate(async (valid) => {
          if (valid) {
            const { msg } = await getTreeList();
            this.$baseMessage(msg, "success");
            this.treeDialogVisible = false;
            this.getTreeListFuc(0);
          }
        });
      },
      // 设置节点选中
      setCheckedKeys() {
        this.$refs.demoTree.setCheckedKeys([1]);
      },
      // 点击叶子节点
      nodeClick(data, node, el) {},
      // 节点选中操作
      checkNode(data, node, el) {
        this.checkNodeKeys = node.checkedKeys;
      },
      // 节点展开操作
      nodeExpand(data, node, el) {
        this.defaultExpendedKeys.push(data.id);
      },
      // 节点关闭操作
      nodeCollapse(data, node, el) {
        this.defaultExpendedKeys.splice(
          this.defaultExpendedKeys.findIndex((item) => item.id === data.id),
          1
        );
      },
      async loadNode(node, resolve) {
        if (node.level === 0) {
          const { data } = await getTreeList();
          this.loading = false;
          return resolve(data);
        } else {
          const { data } = await getTreeList();
          return resolve(res.data);
        }
      },
      //懒加载树输入框筛选方法

      /* 单选/多选树方法-------------------开始 */
      // 初始化单选树的值

      // 清除单选树选中

      /* 清空选中样式 */
      clearSelected() {
        const allNode = document.querySelectorAll(
          "#singleSelectTree .el-tree-node"
        );
        allNode.forEach((element) => element.classList.remove("is-current"));
      },
      // select多选时移除某项操作
      removeSelectTreeTag(val) {
        const stack = JSON.parse(JSON.stringify(this.selectTreeData));
        while (stack.length) {
          const curr = stack.shift();
          if (curr.name == val) {
            return this.$refs.multipleSelectTree.setChecked(curr.id, false);
          }
          if (curr.children && curr.children.length) {
            stack.unshift(...curr.children);
          }
        }
      },
      changeMultipleSelectTreeHandle(val) {},
      // 点击叶子节点
      selectTreeNodeClick(data, node, el) {
        if (data.rank >= this.selectLevel) {
          this.singleSelectTreeVal = data.name;
          this.singleSelectTreeKey = data.id;
          this.$refs.singleTree.blur();
        }
      },
      // 节点选中操作
      multipleSelectTreeCheckNode(data, node, el) {
        const checkedNodes = this.$refs.multipleSelectTree.getCheckedNodes();
        const keyArr = [];
        const valueArr = [];
        checkedNodes.forEach((item) => {
          if (item.rank >= this.selectLevel) {
            keyArr.push(item.id);
            valueArr.push(item.name);
          }
        });
        this.multipleSelectTreeVal = valueArr;
        this.multipleSelectTreeKey = keyArr.join(",");
      },
      /* 单选/多选树方法-------------------结束 */
    },
  };
</script>
