<template>
  <div class="login-container">
    <div class="login-box">
      <div class="logo-section">
        <img :src="logoImage" alt="Just Eat It Logo" class="logo">
      </div>
      <div class="form-section">
        <form @submit.prevent="handleLogin" class="login-form">
          <div class="form-group">
            <input type="email" v-model="email" placeholder="이메일" required>
          </div>
          <div class="form-group">
            <input type="password" v-model="password" placeholder="비밀번호" required>
          </div>
          <button type="submit" class="login-button">로그인</button>
          <div class="additional-links">
            <router-link to="/signup" class="text-button">회원가입</router-link>
            <span class="divider">|</span>
            <router-link to="/reset-password" class="text-button">비밀번호 찾기</router-link>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import logoImage from '../assets/logo.png'

export default {
  name: 'Login',
  data() {
    return {
      email: '',
      password: '',
      logoImage
    }
  },
  methods: {
    handleLogin() {
      // 로그인 로직 구현
      console.log('로그인 시도:', this.email)
    }
  }
}
</script>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: white;
}

.login-box {
  background-color: white;
  padding: 5rem;
  border-radius: 15px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 1600px;
  display: flex;
  align-items: center;
  gap: 3rem;
}

.logo-section {
  flex: 0.5;
  display: flex;
  align-items: center;
  justify-content: center;
  border-right: 1px solid #eee;
  padding-right: 2rem;
}

.form-section {
  flex: 1.5;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding-left: 2rem;
}

.logo {
  width: 200px;
  display: block;
}

.login-form {
  width: 100%;
  max-width: 800px;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  width: 100%;
}

input {
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 17px;
  width: 100%;
  box-sizing: border-box;
  height: 60px;
}

.login-button {
  background-color: #000;
  color: white;
  padding: 0;
  border: none;
  border-radius: 8px;
  font-size: 17px;
  cursor: pointer;
  transition: background-color 0.3s;
  margin-top: 1rem;
  width: 100%;
  box-sizing: border-box;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.login-button:hover {
  background-color: #333;
}

.additional-links {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1.5rem;
  margin-top: 1rem;
  white-space: nowrap;
}

.text-button,
.router-link-active {
  background: none;
  border: none;
  color: #666;
  font-size: 14px;
  cursor: pointer;
  padding: 5px;
  transition: color 0.3s;
  text-decoration: none;
}

.text-button:hover,
.router-link-active:hover {
  color: #000;
}

.divider {
  color: #ddd;
}

@media (max-width: 768px) {
  .login-box {
    flex-direction: column;
    gap: 3rem;
    max-width: 500px;
    padding: 3rem;
  }

  .logo-section {
    flex: none;
    justify-content: center;
    border-right: none;
    border-bottom: 1px solid #eee;
    padding-right: 0;
    padding-bottom: 2rem;
  }

  .form-section {
    flex: none;
    padding-left: 0;
    justify-content: center;
  }

  .logo {
    width: 150px;
  }

  .login-form {
    max-width: 100%;
  }
}
</style> 