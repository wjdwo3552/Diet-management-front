<template>
  <div v-if="showIntro" class="screen" :class="{ 'fade-out': fadeOut }">
    <div class="image-wrapper">
      <img class="image" src="/인트로 로고.png" alt="인트로 로고" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showIntro: true,
      fadeOut: false,
    };
  },
  mounted() {
    // 2초 대기 후 페이드아웃 시작
    setTimeout(() => {
      this.fadeOut = true;
      // 페이드아웃 끝난 후 페이지 이동
      setTimeout(() => {
        this.showIntro = false;
        this.$router.push("/mainpage");
      }, 1000); // 페이드아웃 지속 시간과 동일
    }, 2000); // 인트로 보여주는 시간
  },
};
</script>

<style scoped>
/* 인트로 화면 */
.screen {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background-color: #ffffff;
  position: fixed;
  top: 0;
  left: 0;
  transition: opacity 1s ease-in-out;
  opacity: 1;
}

/* 페이드아웃 효과 */
.fade-out {
  opacity: 0;
}

/* 로고 이미지 크기 */
.image-wrapper {
  width: 530px;
  height: 445px;
}

.image {
  width: 100%;
  height: 100%;
  object-fit: contain;
}
</style>
