<template>
  <div class="reset-container">
    <div class="reset-box">
      <div class="logo-section">
        <img :src="logoImage" alt="Just Eat It Logo" class="logo">
      </div>
      <div class="form-section">
        <form @submit.prevent="handleResetPassword" class="reset-form">
          <h2 class="form-title">비밀번호 찾기</h2>
          <p class="form-description">가입한 이메일을 입력하시면 인증번호를 보내드립니다.</p>
          <div class="form-group">
            <input type="email" v-model="email" placeholder="이메일" required>
          </div>
          <button type="button" class="send-button" @click="sendVerificationCode" :disabled="isCodeSent">
            {{ isCodeSent ? '인증번호 재전송' : '인증번호 받기' }}
          </button>
          <div class="form-group" v-if="isCodeSent">
            <input type="text" v-model="verificationCode" placeholder="인증번호 6자리" required>
          </div>
          <button type="submit" class="reset-button" :disabled="!isCodeSent">비밀번호 확인</button>
          <div class="additional-links">
            <router-link to="/login" class="text-button">로그인 페이지로 이동</router-link>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import logoImage from '../assets/logo.png'

export default {
  name: 'ResetPassword',
  data() {
    return {
      email: '',
      verificationCode: '',
      isCodeSent: false,
      logoImage
    }
  },
  methods: {
    validateEmail(email) {
      const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      return re.test(email)
    },
    sendVerificationCode() {
      if (!this.validateEmail(this.email)) {
        alert('올바른 이메일 주소를 입력해주세요.')
        return
      }
      console.log('인증번호 전송 시도:', this.email)
      this.isCodeSent = true
    },
    handleResetPassword() {
      if (!this.validateEmail(this.email)) {
        alert('올바른 이메일 주소를 입력해주세요.')
        return
      }
      if (this.verificationCode.length !== 6) {
        alert('6자리 인증번호를 입력해주세요.')
        return
      }
      console.log('비밀번호 확인 시도:', {
        email: this.email,
        verificationCode: this.verificationCode
      })
    }
  }
}
</script>

<style scoped>
.reset-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: white;
}

.reset-box {
  background-color: white;
  padding: 4rem;
  border-radius: 15px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 1400px;
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
  width: 180px;
  display: block;
}

.reset-form {
  width: 100%;
  max-width: 700px;
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
}

.form-title {
  font-size: 24px;
  color: #333;
  margin: 0;
  margin-bottom: 0.5rem;
}

.form-description {
  font-size: 16px;
  color: #666;
  margin: 0;
  margin-bottom: 1rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  width: 100%;
}

input[type="email"],
input[type="text"] {
  padding: 18px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 16px;
  width: 100%;
  box-sizing: border-box;
  height: 55px;
}

.send-button {
  background-color: #666;
  color: white;
  padding: 0;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
  width: 100%;
  box-sizing: border-box;
  height: 55px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.send-button:hover:not(:disabled) {
  background-color: #555;
}

.send-button:disabled {
  background-color: #999;
  cursor: not-allowed;
}

.reset-button {
  background-color: #000;
  color: white;
  padding: 0;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
  margin-top: 1.2rem;
  width: 100%;
  box-sizing: border-box;
  height: 55px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.reset-button:hover:not(:disabled) {
  background-color: #333;
}

.reset-button:disabled {
  background-color: #999;
  cursor: not-allowed;
}

.additional-links {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1.5rem;
  margin-top: 1rem;
  white-space: nowrap;
}

.text-button {
  background: none;
  border: none;
  color: #666;
  font-size: 14px;
  cursor: pointer;
  padding: 5px;
  transition: color 0.3s;
  white-space: nowrap;
  text-decoration: none;
}

.text-button:hover {
  color: #000;
}

@media (max-width: 768px) {
  .reset-box {
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

  .reset-form {
    max-width: 100%;
  }

  .form-title {
    text-align: center;
  }

  .form-description {
    text-align: center;
  }
}
</style> 