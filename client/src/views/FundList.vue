<template>
  <div class="fillcontain">
    <div>
      <el-form :inline="true" ref="add_data">
        <el-form-item class="btnRight">
          <el-button type="primary" size="small" icon="view" @click="handleAdd()">添加</el-button>
        </el-form-item>
      </el-form>
    </div>
    <div class="table_container">
      <el-table v-if="tableData.length>0" :data="tableData" style="width: 100%" max-height="450" border>
        <el-table-column type="index" label="序号" align="center" width="70">
        </el-table-column>
        <el-table-column label="创建时间" align='center' width="250" prop="date">
          <template slot-scope="scope">
            <i class="el-icon-time"></i>
            <span style="margin-left: 10px">{{ scope.row.date }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="type" label="收支类型" align='center' width="150">
        </el-table-column>
        <el-table-column prop="describe" label="收支描述" align='center' width="180">
        </el-table-column>
        <el-table-column prop="income" label="收入" align='center' width="150">
          <template slot-scope="scope">
            <span style="color: #00d053">{{ scope.row.income }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="expend" label="支出" align='center' width="180">
          <template slot-scope="scope">
            <span style="color: #f56767">{{ scope.row.expend }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="cash" label="账户现金" align='center' width="150">
          <template slot-scope="scope">
            <span style="color: #3db3ff">{{ scope.row.cash }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="remark" label="备注" align='center' width="180">
        </el-table-column>
        <el-table-column prop="operation" label="操作" align='center' fixed="right" width="320">
          <template slot-scope="scope">
            <el-button type="warning" icon="edit" size="small" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
            <el-button icon="delete" size="small" type="danger" @click="handleDelete(scope.$index, scope.row)">删除</el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <Dialog-fund :dialog="dialog" @update="getProfile"></Dialog-fund>
  </div>
</template>

<script>
import DialogFund from "../components/DialogFund";
export default {
  name: "fundList",
  components: {
    DialogFund
  },
  data() {
    return {
      tableData: [],
      dialog: {
        show: false
      }
    };
  },
  created() {
    this.getProfile();
  },
  methods: {
    handleAdd() {
      this.dialog.show = true;
    },
    handleEdit(index, row) {
      console.log(123);
    },
    handleDelete(index, row) {
      console.log(456);
    },
    getProfile() {
      //获取表格数据;
      this.$axios
        .get("/api/profiles")
        .then(res => {
          //   console.log(res);
          this.tableData = res.data;
        })
        .catch(err => console.log(err));
    }
  }
};
</script>


<style scoped>
.fillcontain {
  width: 100%;
  height: 100%;
  padding: 16px;
  box-sizing: border-box;
}

.btnRight {
  float: right;
}

.pagination {
  text-align: right;
  margin-top: 10px;
}
</style>