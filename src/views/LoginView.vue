<template>
  <el-form
    ref="formRef"
    style="max-width: 600px"
    :model="numberValidateForm"
    label-width="auto"
    class="demo-ruleForm"
  >
    <el-form-item
      label="账号"
      prop="username"
      :rules="[{ required: true, message: '账号不能为空' }]"
    >
      <el-input v-model="numberValidateForm.username" type="text" autocomplete="off" />
    </el-form-item>
    <el-form-item
      label="密码"
      prop="password"
      :rules="[{ required: true, message: '密码不能为空' }]"
    >
      <el-input v-model="numberValidateForm.password" type="password" autocomplete="off" />
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="submitForm(formRef)">Submit</el-button>
      <el-button @click="resetForm(formRef)">Reset</el-button>
    </el-form-item>
  </el-form>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { ElMessage } from 'element-plus'

const router = useRouter()

const formRef = ref()

const numberValidateForm = ref({
  username: '',
  password: '',
})

const submitForm = (formEl) => {
  if (!formEl) return
  formEl.validate((valid) => {
    if (valid) {
      if (
        numberValidateForm.value.username === 'www' &&
        numberValidateForm.value.password === '111'
      ) {
        ElMessage.success('登录成功')
        router.replace('/logon')
      } else {
        ElMessage.error('用户名或者密码错误.')
      }
    } else {
      console.log('error submit!')
    }
  })
}

const resetForm = (formEl) => {
  if (!formEl) return
  formEl.resetFields()
}
</script>
