<template>
	<div id="login">
    <img style="margin: 0 auto;display: block;" src="../assets/logo.png">
		<el-form ref="login" :model="login_data" :rules="login_rules" 
		 	@keyup.enter.native="submitForm('login')"
			label-width="100px" class="login-form">
			<el-form-item prop="account" label="用户名" :maxlength="12">
				<el-input v-model="login_data.account">
				</el-input>
			</el-form-item>
			<el-form-item prop="password" label="密码" :maxlength="16">
				<el-input type="password" v-model="login_data.password">
				</el-input>
			</el-form-item>
			<el-form-item>
				<el-button type="primary" @click="submitForm('login')" :disabled="btnSureDisabled">确认</el-button>
				<el-button @click="resetForm('login')">重置</el-button>
			</el-form-item>
		</el-form>
	</div>
</template>

<!-- <style lang="scss" type="text/css">
	#login{

		.login-form{
			width: 400px;
			margin: 0 auto;
		}
	}
</style> -->

<script>
// import * as rules from '../plugins/rules'
// import * as api from '../api'

export default {
  name: 'Login',
  props: {
  },
  components: {
  },
  data () {
    return {
      btnSureDisabled: false,
      login_data: {
        account: '',
        password: ''
      },
      searchParams: {}
    }
  },
  computed: {
    login_rules () {
      // return rules.login_rules
      return {}
    }
  },
  watch: {
  },
  mounted () {

  },
  methods: {
    queryChange () {
      let query = this.$route.query

      // 如果是跳转至该页面，那么清除保存的查询条件
      if (Object.keys(query).length > 0) {
        this.clear()

        this.searchParams.status = 'all'

        // 遍历query，并将存在于searchParams key中的值赋值到searchParams中
        Object.keys(query).map(key => {
          if (this.searchParams[key] !== undefined) {
            this.searchParams[key] = query[key]
          }
        })
        // 对于特殊的query额外赋值
        // if (query.is_approved) {
        //   this.searchParams.status = "approved"
        // }
      }
    },
    submitForm (formName) {
      this.$refs[formName].validate((valid) => {
        if (!valid) {
          this.$message.warning('信息未填写完整，请检查')
          return false
        } else {
          // this.btnSureDisabled = true
        }
      })
    },
    resetForm (formName) {
      this.$refs[formName].resetFields()
    }

  }
}
</script>