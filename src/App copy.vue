<template>
    <div id="app">
        <el-card class="login-card">
            <!-- 放置表单容器 -->
            <el-form ref="loginForm" :model="loginForm" :rules="loginRules" style="margin-top:50px">
                <!-- 表单项 -->
                <el-form-item prop="mobile">
                    <!-- 输入框 -->
                    <el-input v-model="loginForm.mobile" placeholder="请输入您的手机号"></el-input>
                </el-form-item>
                <el-form-item prop="password">
                    <!-- 输入框 -->
                    <el-input v-model="loginForm.password" placeholder="请输入您的密码"></el-input>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" style="width: 100%" @click="login">登录</el-button>
                </el-form-item>
            </el-form>
        </el-card>
    </div>
</template>

<script>
export default {
    name: 'App',

    data() {
        const checkMobile = function(rule, value, callback) {
            value.charAt(2) === '9' ? callback() : callback(new Error('手机号第三位必须是9'))
        }
        return {
            loginForm: {
                mobile: '',
                password: '',
            },
            //校验规则
            loginRules: {
                mobile: [
                    { required: true, message: '手机号不能为空', trigger: 'blur' },
                    {
                        message: '手机号格式不正确',
                        pattern: /^1[3-9]\d{9}$/,
                        trigger: 'blur',
                    },
                    {
                        trigger: 'blur',
                        validator: checkMobile,
                    },
                ],
                password: [
                    { required: true, message: '密码不能为空', trigger: 'blur' },
                    { message: '密码的长度应为6-16位', min: 6, max: 16, trigger: 'blur' },
                ],
            },
        }
    },

    mounted() {},

    methods: {
        login() {
            this.$refs.loginForm
                .validate()
                .then(() => console.log('成功'))
                .catch()
        },
    },
}
</script>

<style>
#app {
    width: 100%;
    height: 100vh;
    background-color: pink;
    display: flex;
    justify-content: center;
    align-items: center;
}
.login-card {
    width: 440px;
    height: 300px;
}
</style>
