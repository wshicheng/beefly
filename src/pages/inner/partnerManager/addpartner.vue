<template>
	<div id="addpartner_form">
				<h1 id="addpartner_title">添加合伙人</h1>
			<el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
				  <el-form-item label="姓名" prop="name">
				    <el-input v-model="ruleForm.name" placeholder='请输入姓名'></el-input>
				  </el-form-item>
				  <el-form-item label="性别" prop="sex">
				    <el-radio-group v-model="ruleForm.sex">
				      <el-radio label="男"></el-radio>
				      <el-radio label="女"></el-radio>
				    </el-radio-group>
				  </el-form-item>
				  <el-form-item label="证件类别" prop="IDtype">
				    <el-select v-model="ruleForm.IDtype" placeholder="请选择证件类别">
				      <el-option label="居民身份证" value="居民身份证"></el-option>
				      <el-option label="护照" value="护照"></el-option>
				    </el-select>
				  </el-form-item>
				  <el-form-item label="证件号码" prop="IDcard">
				    <el-input v-model="ruleForm.IDcard" placeholder='请输入证件号码'></el-input>
				  </el-form-item>
				  <el-form-item label="手机号" prop="tel">
				    <el-input v-model="ruleForm.tel" placeholder='请输入手机号'></el-input>
				  </el-form-item>
				  <el-form-item label="车辆数" prop="car">
				    <el-input v-model.number="ruleForm.car" placeholder='请输入车辆数(单位：/辆)'></el-input>
				  </el-form-item>
				  <el-form-item label="邮箱" prop="eamil">
				    <el-input v-model="ruleForm.eamil" placeholder='请输入邮箱'></el-input>
				  </el-form-item>
				  <el-form-item label="通讯地址" prop="address">
				    <el-input v-model="ruleForm.address" placeholder='请输入地址'></el-input>
				  </el-form-item>			  				  
				  <el-form-item label="备注">
				    <el-input type="textarea"></el-input>
				  </el-form-item>
				  <el-form-item>
				    <el-button class='addpartner_button' type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
				    <el-button class='addpartner_button' @click="$router.push({path:'/index/partnerManager'})">取消</el-button>
				  </el-form-item>
				</el-form>
	</div>
</template>
<style scoped>
	#addpartner_form {
		background: #fff;
		padding: 140px 339px 190px 200px;
		margin-right: 20px;
		overflow: hidden;
	}

	.addpartner_button:nth-of-type(1) {
		background: #f87e2b;
		border: none;
	}

	.addpartner_button:nth-of-type(1):hover {
		background: rgba(248,126,43,0.9);
	}


	.addpartner_button:nth-of-type(2):hover {
		border: 1px solid rgb(248,126,43);
		color: rgb(248,126,43);
	}

	.addpartner_button {
		width: 120px;
		height: 50px;
	}

	#addpartner_title {
		position: absolute;
		left: 0px;
		top: 10px;
		padding-left: 20px;
		width: 98%;
		height: 80px;
		font-size: 20px;
		overflow-x: hidden;
		line-height: 72px;
		color: #444;
		border-bottom: 20px solid #f3f3f5;
	}
</style>
      
<script>
export default {
  data () {
    return {
      ruleForm: {
        name: '',
        sex: '女',
        IDtype: '',
        IDcard: '',
        tel: '',
        car: '',
        eamil: '',
        address: ''
      },
      rules: {
        name: [
          { required: true, message: '请输入姓名', trigger: 'blur' },
          { min: 2, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        sex: [
          { required: true, message: '请选择性别', trigger: 'change' }
        ],
        IDtype: [
          { required: true, message: '请选择证件类型', trigger: 'change' }
        ],
        IDcard: [
          { type: 'string', required: true, message: '请输入身份证号码', trigger: 'blur' },
          { min: 15, max: 19, message: '请输入合法的身份证号码', trigger: 'blur' }
        ],
        tel: [
          { type: 'string', required: true, message: '请填写手机号', trigger: 'blur' },
          { min: 11, message: '请输入正确的手机号', trigger: 'blur' }
        ],
        car: [
          { type: 'number', required: true, message: '请填写车辆数', trigger: 'blur' }
        ],
        eamil: [
          { message: '请填写正确邮箱', trigger: 'blur' }
        ],
        address: [
          { required: true, message: '请填写通讯地址', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    submitForm (formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.$confirm('确认添加吗?', '提示', {
            confirmButtonText: '确定',
            cancelButtonText: '信息有误',
            type: 'warning'
          })
        .then(() => {
          this.$message({
            type: 'success',
            message: '添加成功'
          })
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消添加'
          })
        })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    }
  }
}
</script>
