<template>
<!--  <div class="app-container">-->
  <div style="margin: 5px" class="app-container"  label-width="120px">
    <el-form :inline="true" :model="dataForm" @submit.native.prevent >

      <el-col>
      <el-form-item label="地区" prop="address" v-model="ruleForm.address">
        <checkAddress ref="address" v-model="dataForm.address" :form="ruleForm.address" />
      </el-form-item>
        <el-form-item label="年龄">
        </el-form-item>
      <el-form-item>
          <el-input   v-model="dataForm.minage" placeholder="最小年龄" style ="small"></el-input>
      </el-form-item>
      <el-form-item>
        <el-input v-model="dataForm.maxage"  placeholder="最大年龄" style ="small" visibility:hidden></el-input>
      </el-form-item>
        <el-form-item label="身高">
        </el-form-item>
        <el-form-item>
          <el-input v-model="dataForm.minheight" placeholder="最小身高" style ="small"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="dataForm.maxheight" placeholder="最大身高" style ="small"></el-input>
        </el-form-item>
        <el-form-item label="学历">
        </el-form-item>
        <el-form-item>
          <el-select v-model="dataForm.Education" placeholder="请选择">
            <el-option
              v-for="item in Education"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </el-form-item>
      </el-col>

      <el-col>
        <el-form-item>
          <el-form-item label="性别">
          </el-form-item>
<!--          <el-radio-group v-model="dataForm.sex">-->
<!--            <el-radio :label="男">男</el-radio>-->
<!--            <el-radio :label="女">女</el-radio>-->
<!--            <el-radio :label="全部">全部</el-radio>-->
<!--          </el-radio-group>-->
          <el-radio v-model="dataForm.sex" label="男">男</el-radio>
          <el-radio v-model="dataForm.sex" label="女">女</el-radio>
          <el-radio v-model="dataForm.sex" label="全部">全部</el-radio>
        </el-form-item>

        <el-form-item label="交友目的">
        </el-form-item>
        <el-form-item>

          <el-select v-model="dataForm.MarriageOption" placeholder="请选择">
            <el-option
              v-for="item in MarriageOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="月薪">
        </el-form-item>
        <el-form-item>
          <el-select v-model="dataForm.worksalaryOption" placeholder="请选择">
            <el-option
              v-for="item in worksalaryOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
          <el-form-item label="元">
          </el-form-item>
        </el-form-item>

        <el-form-item label="职业/行业">
        </el-form-item>
        <el-form-item>
        <el-select v-model="dataForm.workOption" placeholder="请选择职业/行业">
          <el-option
            v-for="item in workOptions"
            :key="item.value"
            :label="item.label"
            :value="item.value">
          </el-option>
        </el-select>
          </el-form-item>
        <el-form-item>
          &nbsp;&nbsp;
      <el-form-item>
        <el-input v-model="dataForm.name" placeholder="姓名" clearable @keyup.enter.native="getDataList()"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button @click="getDataList()">查询</el-button>
        <el-button  type="primary" @click="addOrUpdateHandle()">新增</el-button>
        <el-button  type="danger" @click="deleteHandle()" :disabled="dataListSelections.length <= 0">批量删除</el-button>
<!--        <v-distpicker  style="width: 1%; height: 1% "></v-distpicker>-->
      </el-form-item>
        </el-form-item>
      </el-col>

    </el-form>
    <el-table
      :data="dataList"
      border
      v-loading="dataListLoading"
      @selection-change="selectionChangeHandle"
      @sort-change='tableSortChange'
      style="width: 100%">
      <el-table-column
        type="selection"
        header-align="center"
        align="center"
        width="50">
      </el-table-column>
      <el-table-column
        prop="id"
        header-align="center"
        sortable
        align="center"
        label="主键">
      </el-table-column>
      <el-table-column
        prop="name"
        header-align="center"
        sortable='custom'
        align="center"
        label="名字">
      </el-table-column>
<!--      <el-table-column-->
<!--        prop="age"-->
<!--        header-align="center"-->
<!--        align="center"-->
<!--        label="年龄">-->
<!--      </el-table-column>-->
      <el-table-column
        prop="sex"
        header-align="center"
        sortable
        align="center"
        label="性别">
      </el-table-column>
      <el-table-column
        prop="birthTime"
        header-align="center"
        align="center"
        label="出生日期">
      </el-table-column>
      <el-table-column
        prop="height"
        header-align="center"
        align="center"
        label="身高cm">
      </el-table-column>
      <el-table-column
        prop="weight"
        header-align="center"
        align="center"
        label="体重">
      </el-table-column>
      <el-table-column
        prop="studyBackground"
        header-align="center"
        align="center"
        label="学历">
      </el-table-column>
      <el-table-column
        prop="monthIncome"
        header-align="center"
        align="center"
        label="月薪">
      </el-table-column>
      <el-table-column
        prop="work"
        header-align="center"
        align="center"
        label="职业">
      </el-table-column>
      <el-table-column
        prop="livingAddress"
        header-align="center"
        align="center"
        label="居住地址">
      </el-table-column>
      <el-table-column
        prop="workAddress"
        header-align="center"
        align="center"
        label="工作地址">
      </el-table-column>
      <el-table-column
        prop="nation"
        header-align="center"
        align="center"
        label="民族">
      </el-table-column>
<!--      <el-table-column-->
<!--        prop="isHaveBrother"-->
<!--        header-align="center"-->
<!--        align="center"-->
<!--        label="是否有兄弟姐妹">-->
<!--      </el-table-column>-->
<!--      <el-table-column-->
<!--        prop="isHaveHouse"-->
<!--        header-align="center"-->
<!--        align="center"-->
<!--        label="名下是否有住房">-->
<!--      </el-table-column>-->
      <el-table-column
        prop="homeStatus"
        header-align="center"
        align="center"
        label="家庭情况">
      </el-table-column>
      <el-table-column
        prop="interest"
        header-align="center"
        align="center"
        label="兴趣爱好">
      </el-table-column>
      <el-table-column
        prop="selectingCondition"
        header-align="center"
        align="center"
        label="择偶条件">
      </el-table-column>
      <el-table-column
        prop="phone"
        header-align="center"
        align="center"
        label="电话">
      </el-table-column>
      <el-table-column
        prop="marriageOption"
        header-align="center"
        align="center"
        label="婚姻情况">
      </el-table-column>
      <el-table-column
        fixed="right"
        header-align="center"
        align="center"
        width="150"
        label="操作">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="addOrUpdateHandle(scope.row.id)">修改</el-button>
          <el-button type="text" size="small" @click="deleteHandle(scope.row.id)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      @size-change="sizeChangeHandle"
      @current-change="currentChangeHandle"
      :current-page="pageIndex"
      :page-sizes="[10, 20, 50, 100]"
      :page-size="pageSize"
      :total="totalPage"
      layout="total, sizes, prev, pager, next, jumper">
    </el-pagination>
    <!-- 弹窗, 新增 / 修改 -->
    <add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList"></add-or-update>
  </div>
</template>

<script>
  import AddOrUpdate from './datingpeople-add-or-update'
  import checkAddress from "../checkAddress.vue";
  import request from "@/utils/request";

  export default {
    data () {
      var validatePass = (rule, value, callback) => {

        if (this.ruleForm.address.province == '' || this.ruleForm.address.detail == '') {
          callback(new Error('请输入完整地址'));
        }
        callback();
      };
      return {

        Education:
          [ {
            value: '0',
            label: '高中及以下'
            },
            {
              value: '1',
              label: '大专'
            },
            {
              value: '2',
              label: '本科'
            },
            {
              value: '3',
              label: '研究生'
          },
            {
              value: '4',
              label: '博士'
            },],
        MarriageOptions:
          [{
            value: '不限',
            label: '不限'
          }, {
            value: '已婚',
            label: '已婚'
          }, {
            value: '离异',
            label: '离异'
          }, {
            value: '分居',
            label: '分居'
          }, {
            value: '丧偶',
            label: '丧偶'
          }],
        worksalaryOptions:
          [{
            value: '不限',
            label: '不限'
          }, {
            value: '保密',
            label: '保密'
          }, {
            value: '2000以下',
            label: '2000以下'
          }, {
            value: '2000-3000',
            label: '2000-3000'
          }, {
            value: '5000-8000',
            label: '5000-8000'
          }, {
            value: '8000-10000',
            label: '8000-10000'
          }, {
            value: '10000-20000',
            label: '10000-20000'
          }, {
            value: '20000-50000',
            label: '20000-50000'
          }, {
            value: '50000以上',
            label: '50000以上'
          }],
        workOptions:
          [
            {
              value:'不限',
              label:'不限'
            },
            {
              value:'医生',
              label:'医生'
            },
            {
              value:'法务',
              label:'法务'
            },
            {
              value:'教师',
              label:'教师'
            },
            {
              value:'财务/会计',
              label:'财务/会计'
            },
            {
              value:'设计师',
              label:'设计师'
            },
            {
              value:'空乘人员',
              label:'空乘人员'
            },
            {
              value:'护士',
              label:'护士'
            },
            {
              value:'记者',
              label:'记者'
            },
            {
              value:'学术/研究',
              label:'学术/研究'
            },
            {
              value:'公务员/政府',
              label:'公务员/政府'
            },
            {
              value:'工程师',
              label:'工程师'
            },
            {
              value:'企业高管',
              label:'企业高管'
            },
            {
              value:'秘书/行政',
              label:'秘书/行政'
            },
            {
              value:'传媒/影视',
              label:'传媒/影视'
            },
            {
              value:'咨询/顾问',
              label:'咨询/顾问'
            },
            {
              value:'军人/警察',
              label:'军人/警察'
            },
            {
              value:'消防员',
              label:'消防员'
            },
            {
              value:'模特',
              label:'模特'
            },
            {
              value:'计算机/IT',
              label:'计算机/IT'
            },
            {
              value:'金融/投资',
              label:'金融/投资'
            },
            {
              value:'服务行业',
              label:'服务行业'
            },
            {
              value:'教育/培训',
              label:'教育/培训'
            },
            {
              value:'主管/经理',
              label:'主管/经理'
            },
            {
              value:'加工/制造',
              label:'加工/制造'
            },
            {
              value:'销售/市场',
              label:'销售/市场'
            },
            {
              value:'自由职业者',
              label:'自由职业者'
            },
            {
              value:'农林牧渔',
              label:'农林牧渔'
            },
            {
              value:'学生',
              label:'学生'
            },
            {
              value:'电子/通信',
              label:'电子/通信'
            },
            {
              value:'采购/贸易',
              label:'采购/贸易'
            },
            {
              value:'公关/商务',
              label:'公关/商务'
            },
            {
              value:'翻译',
              label:'翻译'
            },
            {
              value:'私营业主',
              label:'私营业主'
            },
            {
              value:'人力资源',
              label:'人力资源'
            },
            {
              value:'客户服务',
              label:'客户服务'
            },
            {
              value:'司机',
              label:'司机'
            },
            {
              value:'餐饮/旅游',
              label:'餐饮/旅游'
            },
            {
              value:'医疗/护理',
              label:'医疗/护理'
            },
            {
              value:'保健/美容',
              label:'保健/美容'
            },
            {
              value:'生物/制药',
              label:'生物/制药'
            },
            {
              value:'房地产/建筑',
              label:'房地产/建筑'
            },
            {
              value:'仓储/物流',
              label:'仓储/物流'
            },
            {
              value:'体育工作者',
              label:'体育工作者'
            },
            {
              value:'待业中',
              label:'待业中'
            },
            {
              value:'其他行业',
              label:'其他行业'
            }
          ],
        dataForm: {
         name:"",
         sex:"全部",
         address:"",
         minage:"",
         maxage:"",
         minheight:"",
         maxheight:"",
         MarriageOption:"",
         MakefriendOption:"",
         worksalaryOption:"",
         workOption:"",
         monthIncome:""
        },
        dataList: [],
        pageIndex: 1,
        pageSize: 10,
        totalPage: 0,
        dataListLoading: false,
        dataListSelections: [],
        addOrUpdateVisible: false,
        searchParam: [],
        supplierList: [],
        direction: 'btt',
        ifCreate: false,
        ruleForm: {
          address: {
            // 省
            province: "",
            // 市
            city: "",
            // 区
            district: "",
            // 详细地址
            detail: ""
          }
        },
        rules: {
          address: [
            { required: true , validator: validatePass, trigger: 'blur' },
          ]
        }

      }
    },
    components: {
      AddOrUpdate,
      checkAddress
    },
    created() {
      this.getDataList()
    },
    activated () {

    },
    mounted() {

    },
    methods: {
      //按列排序
      tableSortChange(val) {
        console.log(val) // column: {…} order: "ascending" prop: "date"
        // this.queryParams.pageNo = 1
        if (column.order === 'descending') {
          this.queryParams.sortby = val.prop
          this.queryParams.order = 'desc'
        } else {
          this.queryParams.sortby = val.prop
          this.queryParams.order = 'asc'
        }
        if (column.order === 'descending') {
          this.queryParams.sortby = val.prop
          this.queryParams.order = 'desc'
        } else {
          this.queryParams.sortby = val.prop
          this.queryParams.order = 'asc'
        }
        console.log('11111111',this.queryParams.sortby)
        console.log('22222222',this.queryParams.order)
        this.getDataList()
      },

      // 获取数据列表
      getDataList () {
        this.searchParam.length = 0
        this.dataListLoading = true
        this.searchParam.push({
          column: 'name',
          type: 'like',
          // value: 'this.dataForm.name'
          value: this.dataForm.name
        },
          {
          column: 'sex',
          type: 'like',
          value:  this.dataForm.sex === "全部" ? "" : this.dataForm.sex
          // sex: '男'
      },
          {
            column: 'marriageOption',
            type: 'like',
            value:  this.dataForm.MarriageOption
            // value:  '未婚'
            // sex: '男'
          }
          ,
          {
            column: 'workAddress',
            type: 'like',
            value:  this.dataForm.address
            // value:  '新都区'
            // sex: '男'
          }
      )
        if (this.dataForm.worksalaryOption === "不限" || this.dataForm.worksalaryOption === "保密" || this.dataForm.worksalaryOption === "") {

        } else if (this.dataForm.worksalaryOption === "2000以下") {
          this.searchParam.push(
            {
              column: 'monthIncome',
              type: 'le',
              value:  this.dataForm.worksalaryOption
            }
          )
        } else if (this.dataForm.worksalaryOption === "50000以上") {
          this.searchParam.push(
            {
              column: 'monthIncome',
              type: 'ge',
              value:  this.dataForm.worksalaryOption
            }
          )
        } else {
          this.searchParam.push(
            {
              column: 'monthIncome',
              type: 'le',
              value:  this.dataForm.worksalaryOption.split("-")[1]
            }
            ,
            {
              column: 'monthIncome',
              type: 'gt',
              value:  this.dataForm.worksalaryOption.split("-")[0]
            }
          )
        }
        console.log("***************",this.dataForm.worksalaryOption)
        console.log("1111111111111111",this.dataForm.address)
        console.log(this.searchParam)
        return  request({
          url: '/dynxq/datingpeople/list',
          method: 'get',
          params: {
            page: this.pageIndex,
            limit: this.pageSize,
            worksalaryOption: this.dataForm.worksalaryOption,
            condition: JSON.stringify(this.searchParam)
          }
        })
          .then((reponse) => {
          if (data && data.code === 0) {
            this.dataList = data.page.list
            this.totalPage = data.page.totalCount
          } else {
            this.dataList = []
            this.totalPage = 0
          }
          this.dataListLoading = false
        })
      },
      onChangeProv (e) {
        console.log("省", e);
      },
      onChangeCity (e) {
        console.log("市", e);
      },
      onChangeArea (e) {
        console.log("县", e);
      },
      // 每页数
      sizeChangeHandle (val) {
        this.pageSize = val
        this.pageIndex = 1
        this.getDataList()
      },
      // 当前页
      currentChangeHandle (val) {
        this.pageIndex = val
        this.getDataList()
      },
      // 多选
      selectionChangeHandle (val) {
        this.dataListSelections = val
      },
      // 新增 / 修改
      addOrUpdateHandle (id) {
        this.addOrUpdateVisible = true
        this.$nextTick(() => {
          this.$refs.addOrUpdate.init(id)
        })
      },
      // 删除
      deleteHandle (id) {
        var ids = id ? [id] : this.dataListSelections.map(item => {
          return item.id
        })
        this.$confirm(`确定对[id=${ids.join(',')}]进行[${id ? '删除' : '批量删除'}]操作?`, '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.$http({
            url: '/dynxq/datingpeople/delete',
            method: 'post',
            data: this.$http.setData(ids, false)
          }).then(({data}) => {
            if (data && data.code === 0) {
              this.$message({
                message: '操作成功',
                type: 'success',
                duration: 1500,
                onClose: () => {
                  this.getDataList()
                }
              })
            } else {
              this.$message.error(data.msg)
            }
          })
        })
      }
    }
  }
</script>
