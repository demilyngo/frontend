<template>
  <div
    style="display: flex; justify-content: space-around; align-items: center; width: 100%"
    class="pt-2 pb-2"
  >
    <el-button type="primary" size="large" @click="testQuery">
      <el-icon>
        <Plus />
      </el-icon>
      Создать
    </el-button>

    <el-input v-model="searchInput" :prefix-icon="Search" style="width: 30em; height: 35px" />
    <div>
      <el-button type="primary" size="large" @click="registerFormVisible = true">
        Регистрация
      </el-button>
      <el-button size="large" @click="loginFormVisible = true">Логин</el-button>
    </div>

    <el-dialog v-model="loginFormVisible" title="Логин" width="30%" center @closed="clearLoginForm">
      <el-form :model="login">
        <el-form-item label="Логин" label-width="70px">
          <el-input v-model="login.login" />
        </el-form-item>
        <el-form-item label="Пароль" label-width="70px">
          <el-input v-model="login.password" />
        </el-form-item>
      </el-form>
      <template #footer>
        <div>
          <el-button type="primary">Войти</el-button>
        </div>
      </template>
    </el-dialog>

    <el-dialog
      v-model="registerFormVisible"
      title="Регистрация"
      width="40%"
      center
      @closed="clearRegisterForm"
    >
      <el-form :model="login">
        <el-form-item label="Имя пользователя" label-width="140px">
          <el-input v-model="register.nickname" />
        </el-form-item>
        <el-form-item label="Почта" label-width="140px">
          <el-input v-model="register.email" />
        </el-form-item>
        <el-form-item label="Логин" label-width="140px">
          <el-input v-model="register.login" />
        </el-form-item>
        <el-form-item label="Пароль" label-width="140px">
          <el-input v-model="register.password" type="password" show-password />
        </el-form-item>
        <el-form-item label="Повторите пароль" label-width="140px">
          <el-input v-model="register.repeatPassword" type="password" show-password />
        </el-form-item>
      </el-form>
      <template #footer>
        <div>
          <el-button type="primary">Зарегистрироваться</el-button>
        </div>
      </template>
    </el-dialog>
  </div>
</template>
<script setup lang="ts">
import { ref, reactive } from 'vue'
import { Search } from '@element-plus/icons-vue'
import axios from 'axios'

const testQuery = async () => {
  const cats = await axios.get('/api/posts')
  console.log(cats)
}

const searchInput = ref('')

const registerFormVisible = ref(false)

const loginFormVisible = ref(false)

const login = reactive({
  login: '',
  password: ''
})
const register = reactive({
  nickname: '',
  email: '',
  login: '',
  password: '',
  repeatPassword: ''
})
const clearLoginForm = () => {
  login.login = ''
  login.password = ''
}
const clearRegisterForm = () => {
  register.nickname = ''
  register.email = ''
  register.login = ''
  register.password = ''
  register.repeatPassword = ''
}
</script>
<style></style>
