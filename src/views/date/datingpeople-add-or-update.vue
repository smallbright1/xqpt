<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="名字" prop="name">
      <el-input v-model="dataForm.name" placeholder="名字"></el-input>
    </el-form-item>
    <el-form-item label="年龄" prop="age">
      <el-input v-model="dataForm.age" placeholder="年龄"></el-input>
    </el-form-item>
    <el-form-item label="性别" prop="sex">
      <el-input v-model="dataForm.sex" placeholder="性别"></el-input>
    </el-form-item>
    <el-form-item label="出生日期" prop="birthTime">
      <el-input v-model="dataForm.birthTime" placeholder="出生日期"></el-input>
    </el-form-item>
    <el-form-item label="籍贯" prop="birthPlace">
      <el-input v-model="dataForm.birthPlace" placeholder="籍贯"></el-input>
    </el-form-item>
    <el-form-item label="民族" prop="nation">
      <el-input v-model="dataForm.nation" placeholder="民族"></el-input>
    </el-form-item>
    <el-form-item label="政治面貌" prop="politicalStatus">
      <el-input v-model="dataForm.politicalStatus" placeholder="政治面貌"></el-input>
    </el-form-item>
    <el-form-item label="学历" prop="studyBackground">
      <el-input v-model="dataForm.studyBackground" placeholder="学历"></el-input>
    </el-form-item>
    <el-form-item label="专业" prop="mainSubject">
      <el-input v-model="dataForm.mainSubject" placeholder="专业"></el-input>
    </el-form-item>
    <el-form-item label="健康状况" prop="healthStatus">
      <el-input v-model="dataForm.healthStatus" placeholder="健康状况"></el-input>
    </el-form-item>
    <el-form-item label="身高" prop="height">
      <el-input v-model="dataForm.height" placeholder="身高"></el-input>
    </el-form-item>
    <el-form-item label="体重" prop="weight">
      <el-input v-model="dataForm.weight" placeholder="体重"></el-input>
    </el-form-item>
    <el-form-item label="工作地址" prop="workAddress">
      <el-input v-model="dataForm.workAddress" placeholder="工作地址"></el-input>
    </el-form-item>
    <el-form-item label="居住地址" prop="livingAddress">
      <el-input v-model="dataForm.livingAddress" placeholder="居住地址"></el-input>
    </el-form-item>
    <el-form-item label="家庭情况" prop="homeStatus">
      <el-input v-model="dataForm.homeStatus" placeholder="家庭情况"></el-input>
    </el-form-item>
    <el-form-item label="兴趣爱好" prop="interest">
      <el-input v-model="dataForm.interest" placeholder="兴趣爱好"></el-input>
    </el-form-item>
    <el-form-item label="择偶条件" prop="selectingCondition">
      <el-input v-model="dataForm.selectingCondition" placeholder="择偶条件"></el-input>
    </el-form-item>
    <el-form-item label="电话" prop="phone">
      <el-input v-model="dataForm.phone" placeholder="电话"></el-input>
    </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="visible = false">取消</el-button>
      <el-button type="primary" @click="dataFormSubmit()">确定</el-button>
    </span>
  </el-dialog>
</template>

<script>
  export default {
    data () {
      return {
        visible: false,
        dataForm: {
          id: 0,
          name: '',
          age: '',
          sex: '',
          birthTime: '',
          birthPlace: '',
          nation: '',
          politicalStatus: '',
          studyBackground: '',
          mainSubject: '',
          healthStatus: '',
          height: '',
          weight: '',
          workAddress: '',
          livingAddress: '',
          homeStatus: '',
          interest: '',
          selectingCondition: '',
          phone: ''
        },
        dataRule: {
          name: [
            { required: true, message: '名字不能为空', trigger: 'blur' }
          ],
          age: [
            { required: true, message: '年龄不能为空', trigger: 'blur' }
          ],
          sex: [
            { required: true, message: '性别不能为空', trigger: 'blur' }
          ],
          birthTime: [
            { required: true, message: '出生日期不能为空', trigger: 'blur' }
          ],
          birthPlace: [
            { required: true, message: '籍贯不能为空', trigger: 'blur' }
          ],
          nation: [
            { required: true, message: '民族不能为空', trigger: 'blur' }
          ],
          politicalStatus: [
            { required: true, message: '政治面貌不能为空', trigger: 'blur' }
          ],
          studyBackground: [
            { required: true, message: '学历不能为空', trigger: 'blur' }
          ],
          mainSubject: [
            { required: true, message: '专业不能为空', trigger: 'blur' }
          ],
          healthStatus: [
            { required: true, message: '健康状况不能为空', trigger: 'blur' }
          ],
          height: [
            { required: true, message: '身高不能为空', trigger: 'blur' }
          ],
          weight: [
            { required: true, message: '体重不能为空', trigger: 'blur' }
          ],
          workAddress: [
            { required: true, message: '工作地址不能为空', trigger: 'blur' }
          ],
          livingAddress: [
            { required: true, message: '居住地址不能为空', trigger: 'blur' }
          ],
          homeStatus: [
            { required: true, message: '家庭情况不能为空', trigger: 'blur' }
          ],
          interest: [
            { required: true, message: '兴趣爱好不能为空', trigger: 'blur' }
          ],
          selectingCondition: [
            { required: true, message: '择偶条件不能为空', trigger: 'blur' }
          ],
          phone: [
            { required: true, message: '电话不能为空', trigger: 'blur' }
          ]
        }
      }
    },
    methods: {
      init (id) {
        this.dataForm.id = id || 0
        this.visible = true
        this.$nextTick(() => {
          this.$refs['dataForm'].resetFields()
          if (this.dataForm.id) {
            this.$http({
              url: this.$http.setUrl(`/dynxq/datingpeople/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.setParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.name = data.datingPeople.name
                this.dataForm.age = data.datingPeople.age
                this.dataForm.sex = data.datingPeople.sex
                this.dataForm.birthTime = data.datingPeople.birthTime
                this.dataForm.birthPlace = data.datingPeople.birthPlace
                this.dataForm.nation = data.datingPeople.nation
                this.dataForm.politicalStatus = data.datingPeople.politicalStatus
                this.dataForm.studyBackground = data.datingPeople.studyBackground
                this.dataForm.mainSubject = data.datingPeople.mainSubject
                this.dataForm.healthStatus = data.datingPeople.healthStatus
                this.dataForm.height = data.datingPeople.height
                this.dataForm.weight = data.datingPeople.weight
                this.dataForm.workAddress = data.datingPeople.workAddress
                this.dataForm.livingAddress = data.datingPeople.livingAddress
                this.dataForm.homeStatus = data.datingPeople.homeStatus
                this.dataForm.interest = data.datingPeople.interest
                this.dataForm.selectingCondition = data.datingPeople.selectingCondition
                this.dataForm.phone = data.datingPeople.phone
              }
            })
          }
        })
      },
      // 表单提交
      dataFormSubmit () {
        this.$refs['dataForm'].validate((valid) => {
          if (valid) {
            this.$http({
              url: this.$http.setUrl(`/dynxq/datingpeople/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.setData({
                'id': this.dataForm.id || undefined,
                'name': this.dataForm.name,
                'age': this.dataForm.age,
                'sex': this.dataForm.sex,
                'birthTime': this.dataForm.birthTime,
                'birthPlace': this.dataForm.birthPlace,
                'nation': this.dataForm.nation,
                'politicalStatus': this.dataForm.politicalStatus,
                'studyBackground': this.dataForm.studyBackground,
                'mainSubject': this.dataForm.mainSubject,
                'healthStatus': this.dataForm.healthStatus,
                'height': this.dataForm.height,
                'weight': this.dataForm.weight,
                'workAddress': this.dataForm.workAddress,
                'livingAddress': this.dataForm.livingAddress,
                'homeStatus': this.dataForm.homeStatus,
                'interest': this.dataForm.interest,
                'selectingCondition': this.dataForm.selectingCondition,
                'phone': this.dataForm.phone
              })
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.$message({
                  message: '操作成功',
                  type: 'success',
                  duration: 1500,
                  onClose: () => {
                    this.visible = false
                    this.$emit('refreshDataList')
                  }
                })
              } else {
                this.$message.error(data.msg)
              }
            })
          }
        })
      }
    }
  }
</script>
