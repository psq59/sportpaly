<template>
<div class="login_container">
    <div class="login_box">
      <div class="avatar_box">
        <!--头像-->
        <img src="../assets/logo.jpeg" alt />
      </div>
      <!--添加表单-->
    <el-form ref="loginFormRef" 
      	:model="loginForm" 
      	:rules="loginRules"
      	class="login_form"
      	label-width="80px"
      	>
  		<el-form-item prop="username">
      	 <el-input v-model="loginForm.username" prefix-icon="iconfont icon-denglu-copy
"></el-input>
  		</el-form-item>
  		<el-form-item prop="password">
      	 <el-input v-model="loginForm.password" prefix-icon="iconfont icon-mima" type="password" show-password></el-input>
  		</el-form-item>
  		<el-form-item class="btns">
      	  <el-button type="primary" @click="login">登录</el-button>
          <el-button type="info" @click="resetLoginForm">重置</el-button>
  		</el-form-item>
  	</el-form> 
    </div>
    
</div>
</template>

<script>
	export default{
		data(){
			return{
				loginForm:{
					username:"admin",
					password:"123456"
				},
				loginRules:{
					username:[
           				{ required: true, message: '请输入用户名', trigger: 'blur' },
            			{ min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
            		],
					password:[
						{required:true,message:"请输入密码",trigger:"blur"},
						{min:6,max:8,message:"密码为6~8位",trigger:"blur"}
					]
				}
			};
		},
		 methods: {
    		resetLoginForm() {
      			this.$refs.loginFormRef.resetFields();
    		},
    		login() {
      			this.$refs.loginFormRef.validate(async valid => {
        		if (!valid) return;
        		// 调用get请求
        		const {data :res} = await this.$http.post("test");
         		if (res == "ok" ) {
           		this.$message.success("登陆成功");
           		this.$router.push({ path: "/home"});// 路由
         	}else{
          		this.$message.error("登录失败");
         }
      });
    }
  }
	};
</script>

<style lang="less" scoped="scoped">
.login_container{
	background-color: #2B4B6B;
	height: 100%;
}
.login_box{
	width: 450px;
	height: 300px;
	background-color: #FFFFFF;
	border-radius: 3px;/*圆角*/
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%,-50%);
	.avatar_box{
		width: 130px;
		height: 130px;
		border: 1px solid #EEEEEE;
		border-radius: 50%;
		padding: 10px;
		box-shadow: 0 0 10px #ddd;/*盒子阴影*/
		position: absolute;
		left: 50%;
		transform: translate(-50%,-50%);
		background:#EEEEEE;
		img{
			width: 100%;
			height: 100%;
			border-radius: 30%;
		}
	}
}
.btns{
	display: flex;
	justify-content: flex-end;/*尾部对齐*/
}
.login_form{
	position: absolute;
	bottom: 0%;
	width:100%;
	right: 8%;
	box-sizing: border-box;
}
</style>