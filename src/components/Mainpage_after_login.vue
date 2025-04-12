<template>
  <div class="div-wrapper">
    <div class="div">
      <img class="image" :src="mainLogo" alt="메인 로고" />

      <div class="text-wrapper">
        <router-link to="/mypage" class="login-link" translate="no">내 정보</router-link>
      </div>

      <div class="logout-wrapper">
        <button @click="handleLogout" class="logout-button" aria-label="로그아웃" title="로그아웃">
          <img :src="logoutIcon" alt="로그아웃 아이콘" class="logout-icon" />
        </button>
      </div>

      <div class="view" @click="focusSearchInput">
        <div class="overlap-group">
          <div class="search-input-container">
            <img class="img" :src="searchIcon" alt="검색 아이콘" />
            <input ref="searchInput" class="search-input" type="text" translate="no" placeholder="검색어를 입력하세요" />
          </div>
        </div>
      </div>
    </div>

    <div class="navbar">
      <div class="text-wrapper-3" translate="no">식단 추천</div>
      <div class="text-wrapper-4" translate="no">식단 일기</div>
      <div class="text-wrapper-5" translate="no">영양 진단기</div>
    </div>

    <p class="p" translate="no">JUST EAT IT과 함께 스마트한 식단관리를 시작하세요</p>
  </div>
</template>

<script>
import mainLogo from "@/assets/메인페이지 로고1.png";
import searchIcon from "@/assets/검색 아이콘.png";
import logoutIcon from "@/assets/logout-icon.png";

export default {
  name: "mainPage_after_login",
  data() {
    return {
      mainLogo,
      searchIcon,
      logoutIcon
    };
  },
  methods: {
    focusSearchInput() {
      this.$refs.searchInput.focus();
    },
    handleLogout() {
      this.$router.push('/mainpage');
    }
  }
};
</script>

<style scoped>
@font-face {
  font-family: "Esamanru-Bold";
  src: url("@/assets/font/esamanru Bold.ttf") format("truetype");
  font-weight: bold;
}

@font-face {
  font-family: "Esamanru-Light";
  src: url("@/assets/font/esamanru Light.ttf") format("truetype");
  font-weight: 300;
}

@font-face {
  font-family: "Esamanru-Medium";
  src: url("@/assets/font/esamanru Medium.ttf") format("truetype");
  font-weight: 500;
}

.div-wrapper {
  width: 100%;
  min-width: 1200px;
  max-width: 1440px;
  margin: 0 auto;
  height: 100vh;
  position: relative;
  background-color: #ffffff;
}

.div {
  width: 100%;
  height: 100%;
  position: relative;
  background-color: #ffffff;
}

.image {
  position: absolute;
  width: 400px;
  height: 400px;
  top: 220px;
  left: 1000px;
  object-fit: cover;
}

.text-wrapper {
  position: absolute;
  top: 25px;
  left: 1320px;
  font-size: 25px;
  font-family: "Esamanru-Light", sans-serif;
  font-weight: 300;
  white-space: nowrap;
  overflow: visible;
}

.login-link {
  text-decoration: none;
  color: inherit;
}

.view {
  position: absolute;
  width: 500px;
  height: 50px;
  top: 15px;
  left: 750px;
}

.overlap-group {
  position: relative;
  width: 500px;
  height: 45px;
  background-color: #ffffff80;
  border-radius: 20px;
  border: 3px solid #000000;
}

.img {
  position: absolute;
  width: 20px;
  height: 25px;
  top: 7px;
  left: 11px;
}

.search-input {
  width: 100%;
  height: 41px;
  padding-left: 40px;
  font-family: "Esamanru-Light", sans-serif;
  font-size: 18px;
  border: none;
  outline: none;
  background-color: transparent;
}

.search-input-container {
  position: relative;
  display: flex;
  align-items: center;
  width: 100%;
}

.search-input:focus {
  border-bottom: none;
}

.navbar {
  position: absolute;
  top: 25px;
  left: 150px;
  display: flex;
  gap: 50px;
  font-family: "Esamanru-Light", sans-serif;
  font-weight: 300;
  font-size: 30px;
}

.navbar > div {
  cursor: pointer;
}

.text-wrapper-3,
.text-wrapper-4,
.text-wrapper-5 {
  position: static;
  font-family: "Esamanru-Light", sans-serif;
  font-weight: 300;
  font-size: 25px;
}

.text-wrapper-3 { left: 0; }
.text-wrapper-4 { left: 176px; }
.text-wrapper-5 { left: 352px; }

.p {
  position: absolute;
  top: 150px;
  left: 30px;
  font-family: "Esamanru-Bold", sans-serif;
  font-weight: 700;
  font-size: 35px;
}

.user-links {
  position: absolute;
  top: 25px;
  left: 1250px;
  display: flex;
  gap: 20px;
  align-items: center;
}

.logout-button {
  background-color: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
}

.logout-button:hover {
  text-decoration: underline;
}

.logout-wrapper {
  position: absolute;
  top: 26px;
  right: -10px;
}

.logout-icon {
  width: 25px;
  height: 25px;
}
</style>
