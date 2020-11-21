<template>
  <div>
    <el-button @click="dialogFormVisible = true" style="float: left;margin-bottom: 10px;" icon="el-icon-circle-plus-outline">
      添加坐席
    </el-button>
    <el-table
      :data="tableData"
      style="width: 100%">

      <el-table-column
        prop="userName"
        label="坐席名称"
        align="center">
      </el-table-column>
      <el-table-column
        prop="bindPhone"
        label="手机号码"
        align="center">
      </el-table-column>
      <el-table-column
        prop="userCode"
        label="坐席编号"
        align="center">
      </el-table-column>
      <el-table-column
        prop="waitTime"
        label="等待时长(s)"
        align="center">
      </el-table-column>
      <el-table-column
        fixed="right"
        label="操作"
        type="index"
        align="center"
        width="200"
        >
        <template slot-scope="scope">
          <el-button @click="handleClick(scope)" type="text" size="small">修改坐席</el-button>
          <el-button @click="deleteService(scope)" type="text" size="small">删除</el-button>
          <!--<el-button @click="seeUserInfoAppList(scope)" type="text" size="small">查看业绩</el-button>-->
          <!--<el-button type="text" size="small">编辑</el-button>-->
        </template>
      </el-table-column>
    </el-table>
    <el-dialog title="添加坐席" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item
          label="坐席名称"
          :label-width="formLabelWidth"
          prop="username"
        >
          <el-input v-model.string="form.username"  auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item
          label="绑定手机号"
          :label-width="formLabelWidth"
          prop="username"
        >
          <el-input v-model.string="form.phone"  auto-complete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="submitData">确 定</el-button>
      </div>
    </el-dialog>
    <el-dialog title="修改坐席" :visible.sync="editFlag">
      <el-form :model="form">
        <el-form-item
          label="坐席名称"
          :label-width="formLabelWidth"
          prop="username"
        >
          <el-input v-model.string="editForm.userName"  auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item
          label="绑定手机号"
          :label-width="formLabelWidth"
          prop="username"
        >
          <el-input v-model.string="editForm.bindPhone"  auto-complete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="editFlag = false">取 消</el-button>
        <el-button type="primary" @click="submitDataEdit">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
  import 'quill/dist/quill.core.css';
  import 'quill/dist/quill.snow.css';
  import 'quill/dist/quill.bubble.css';
  export default {
    data() {
      return {
        editFlag:false,
        dialogFormVisible: false,
        form:{
          username:'',
          phone:'',
        },
        editForm:{
          phone:'',
          username:''
        },
        orgId:JSON.parse(localStorage.getItem('userinfo')).id,
        formLabelWidth: '120px',

        tableData: [],
        total:0
      }
    },
    created:function () {
      this.getVendorList();

    },
    methods:{
      getVendorList(){
          this.http.post('/api/selectSysZerroSeatsAll',{orgId:this.orgId}).then(res=>{
          if(res.code == 0){
            this.tableData = res.data;
          }else{
            this.tableData = [];
          }
        })
      },
      handleClick(data){
        this.editFlag = true
        this.editForm = data.row;
      },
      submitData(){
        if(!this.form.username) {
          this.$errorMessage('请填写坐席名称')
          return;
        }
        this.form.orgId = this.orgId;
        this.http.post('/api/insertSysZerroSeats',this.form).then(res=>{
          if(res.code == 0){
              this.$successMessage('添加成功');
              this.dialogFormVisible = false;
              this.getVendorList();
          }
        })
      },
      submitDataEdit(){
        if(!this.editForm.userName) {
          this.$errorMessage('请填写坐席名称')
          return;
        }
        if(!this.editForm.bindPhone) {
          this.$errorMessage('请填写坐席绑定手机号')
          return;
        }
        this.editForm.orgId = this.orgId;
        this.http.post('/api/updateSysZerroSeats',this.editForm).then(res=>{
          if(res.code == 0){
            this.$successMessage('修改成功');
            this.editFlag = false;
            this.getVendorList();
          }
        })
      },

      deleteService(data){
        this.$confirm('确定删除此条数据吗', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(async () => {
          await this.deleteServiceFn(data.row);
        }).catch(() => {
        });
      },
      deleteServiceFn(data){
        this.http.post('/api/deleteSysZerroSeats',{agentId:data.agentId,orgId:this.orgId}).then(res=>{
          if(res.code == 0){
            this.$successMessage('已删除')
            this.getVendorList();
          }
        })
      },
    },
  }
</script>

<style>
  .el-main{
    line-height: 30px !important;
  }
  .ql-container{
    height: 200px;
  }
  .ql-snow .ql-picker:not(.ql-color-picker):not(.ql-icon-picker) svg{
    margin-top: 0px;
  }
</style>
