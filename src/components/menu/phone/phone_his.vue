<template>
  <div style="padding: 20px;">
    <div>
      <el-select v-model="searchForm.type" placeholder="请选择接听状态" >
        <el-option label="不限" value="" >
          不限
        </el-option>
        <el-option label="未接听" value="ERROR" >
          未接听
        </el-option>
        <el-option label="未接听" value="SUCCESS" >
          已接听
        </el-option>
      </el-select>


      <el-date-picker
        v-model="setTime"
        type="datetimerange"
        value-format="yyyy-MM-dd HH:mm:ss"
        range-separator="至"
        start-placeholder="开始日期"
        end-placeholder="结束日期">
      </el-date-picker>
      <el-button @click="searchOrders" type="primary">搜索</el-button>
    </div>
    <el-table
      :data="hisList"
      style="width: 100%;margin-top: 10px;">
      <el-table-column
        prop="callerno"
        label="呼入号码"
        align="center">
      </el-table-column>
      <el-table-column
        prop="district"
        label="地区"
        align="center">
      </el-table-column>

      <el-table-column
        prop="seatsName"
        label="接听坐席"
        align="center">
      </el-table-column>
      <el-table-column
        prop="talkLen"
        label="通话时长"
        align="center">
      </el-table-column>
      <el-table-column
        prop="talkTime"
        label="接入时间"
        align="center">
      </el-table-column>
      <el-table-column
        prop="talkTime"
        label="通话状态"
        align="center">
        <template slot-scope="scope">
          <span style="color:green" v-if="scope.row.type == 'SUCCESS'">已接听</span>
          <span style="color:red" v-if="scope.row.type == 'ERROR'">未接听</span>
        </template>
      </el-table-column>
      <el-table-column
        label="操作"
        type="index"
        align="center"
        width="180"
      >
        <template slot-scope="scope">
          <el-button icon="el-icon-mic" @click="getRecordFileUrl(scope.row)" type="primary" size="mini">查看录音</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      @current-change="handleCurrentChangeSys"
      :current-page="searchForm.pageNum"
      layout="total, prev, pager, next, jumper"
      :total="total">
    </el-pagination>
    <el-dialog title="查看录音" width="50%" :visible.sync="listenFlag">
      <div>
        <audio id="audio" preload="auto" controls="" ><source :src="listenUrl" type="audio/mpeg"><embed :src="listenUrl"></audio>
      </div>
      <div slot="footer" class="dialog-footer">
        <el-button @click="closeListen">取 消</el-button>
      </div>
    </el-dialog>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        setTime: '',
        orgList: [],
        hisList: [],
        total: 0,
        listenFlag: false,
        searchForm: {
          pageNum: 1,
          startTime:'',
          endTime:'',
          pageSize: 10,
          orgId:'',
          type:''
        },
        listenUrl:'', //录音地址

      }
    },
    created() {
      this.searchForm.orgId = this.$store.state.user.user.id;
      this.getPhoneHisList();
    },
    methods: {
      //关闭录音查看
      closeListen(){
        document.getElementById('audio').pause();
        this.listenUrl = '';
        this.listenFlag = false;
      },
      //查看录音
      getRecordFileUrl(data){
        var obj  = {
          lsh:data.talkNum,
          date:data.talkTime.split(' ')[0]
        }
        this.http.post('/api/getRecordFileUrl', obj).then(res => {
          if (res.code == 0) {
            if(res.data!='0'){
              this.listenFlag = true;
              this.listenUrl = res.data;
              this.$nextTick(()=>{
                document.getElementById('audio').load()
              })
            }else{
              this.$errorMessage('此通话记录没有录音')
            }

          }
        })
      },
      //搜索记录筛选
      searchOrders() {
        if(this.setTime && this.setTime.length>0){
          this.searchForm.startTime = this.setTime[0];
          this.searchForm.endTime = this.setTime[1];
        }
        this.searchForm.pageNum = 1;
        this.getPhoneHisList();
      },
      //获取搜索记录
      getPhoneHisList() {
        this.http.post('/api/querySeatsDetail', this.searchForm).then(res => {
          if (res.code == 0) {
            this.hisList = res.data.list;
            this.total = Number(res.data.total);
          }
        })
      },
      handleCurrentChangeSys(val) {
        this.searchForm.pageNum = val;
        this.getPhoneHisList();
      },
    },
  }
</script>
<style>
  .el-main {
    line-height: 30px !important;
  }
</style>
