<template>
  <div class="div-wrapper">
    <div class="div">
      <img class="image" :src="mainLogo" alt="메인 로고" />

      <div class="text-wrapper">
        <router-link to="/login" class="login-link" translate="no">로그인</router-link>
      </div>

      <div class="view" @click="focusSearchInput">
        <div class="overlap-group">
          <div class="search-input-container">
            <img class="img" :src="searchIcon" alt="검색 아이콘" />
            <input ref="searchInput" class="search-input" type="text" translate="no" placeholder="검색어를 입력하세요" />
          </div>
        </div>
      </div>

      <div class="navbar">
        <div class="text-wrapper-3" translate="no">식단 추천</div>
        <div class="text-wrapper-4" translate="no" @click="showLoginRequiredModal">식단 일기</div>
        <div class="text-wrapper-5" translate="no" @click="showLoginRequiredModal">영양 진단기</div>
      </div>

      <p class="p" translate="no">JUST EAT IT과 함께 스마트한 식단관리를 시작하세요</p>

      <div class="today-meal-section">
        <h2 class="section-title" translate="no">
          <img :src="recommendIcon" alt="식단 추천 아이콘" class="recommend_icon">
          오늘은 이 식단 어때요?
        </h2>
        <div class="carousel-wrapper">
          <button class="slide-button left" @click="scrollLeft" @mouseenter="stopAutoSlide" @mouseleave="startAutoSlide">‹</button>
          <div class="carousel" ref="carousel">
            <div class="card" v-for="(meal, index) in visibleMeals" :key="index" @mouseenter="stopAutoSlide" @mouseleave="startAutoSlide">
              <img :src="meal.image" alt="식단 이미지" class="card-image" />
              <div class="card-content">
                <h3 class="meal-title" translate="no">{{ meal.title }}</h3>
                <p class="meal-desc" translate="no">{{ meal.description }}</p>
              </div>
            </div>
          </div>
          <button class="slide-button right" @click="scrollRight" @mouseenter="stopAutoSlide" @mouseleave="startAutoSlide">›</button>
        </div>
      </div>
    </div>
  </div>

  <div v-if="isModalOpen" class="modal-overlay" @click.self="closeModal">
    <div class="modal-content">
      <button class="modal-close" @click="closeModal">×</button>
      <h2 class="modal-title">로그인이 필요합니다</h2>
      <p class="modal-body" translate="no">확인 버튼을 누르면 로그인페이지로 이동합니다.</p>
      <router-link to="/login">
        <button class="modal-confirm">확인</button>
      </router-link>
    </div>
  </div>
</template>

<script>
import mainLogo from '@/assets/images/logo/main-logo.png';
import searchIcon from '@/assets/images/icon/search.png';
import recommendIcon from '@/assets/images/icon/recommend.png';

export default {
  data() {
    return {
      isModalOpen: false,
      autoSlideInterval: null,
      meals: [
        {
          title: '고단백 닭가슴살 도시락',
          description: '운동 후 회복에 좋은 닭가슴살과 채소 구성',
          image: require('@/assets/images/meals/meal1.jpg')
        },
        {
          title: '채식 위주의 샐러드',
          description: '신선한 채소와 과일로 만든 건강 샐러드',
          image: require('@/assets/images/meals/meal2.jpg')
        },
        {
          title: '균형 잡힌 한식 도시락',
          description: '잡곡밥과 반찬이 조화로운 전통식',
          image: require('@/assets/images/meals/meal3.jpg')
        }
      ]
    };
  },
  computed: {
    visibleMeals() {
      return this.meals;
    }
  },
  mounted() {
    this.startAutoSlide();
  },
  beforeDestroy() {
    this.stopAutoSlide();
  },
  methods: {
    showLoginRequiredModal() {
      this.isModalOpen = true;
    },
    closeModal() {
      this.isModalOpen = false;
    },
    focusSearchInput() {
      this.$refs.searchInput.focus();
    },
    scrollLeft() {
      const carousel = this.$refs.carousel;
      carousel.scrollBy({ left: -300, behavior: 'smooth' });
    },
    scrollRight() {
      const carousel = this.$refs.carousel;
      carousel.scrollBy({ left: 300, behavior: 'smooth' });
    },
    startAutoSlide() {
      this.autoSlideInterval = setInterval(() => {
        this.scrollRight();
      }, 4000);
    },
    stopAutoSlide() {
      clearInterval(this.autoSlideInterval);
      this.autoSlideInterval = null;
    }
  }
};
</script>

<style scoped>
.div-wrapper {
  display: flex;
  justify-content: center;
}

.div {
  width: 100%;
  max-width: 1200px;
  padding: 20px;
}

.image {
  width: 150px;
  margin-bottom: 20px;
}

.login-link {
  float: right;
  font-weight: bold;
}

.view {
  margin: 20px 0;
}

.search-input-container {
  display: flex;
  align-items: center;
  background: #f0f0f0;
  padding: 10px;
  border-radius: 8px;
}

.search-input {
  border: none;
  background: transparent;
  margin-left: 10px;
  width: 100%;
}

.navbar {
  display: flex;
  justify-content: space-around;
  margin: 20px 0;
  font-weight: bold;
}

.p {
  font-size: 18px;
  text-align: center;
  margin-bottom: 30px;
}

.today-meal-section {
  margin-top: 30px;
}

.section-title {
  display: flex;
  align-items: center;
  font-size: 20px;
  margin-bottom: 15px;
}

.recommend_icon {
  width: 24px;
  margin-right: 10px;
}

.carousel-wrapper {
  position: relative;
  overflow: hidden;
}

.carousel {
  display: flex;
  overflow-x: auto;
  scroll-behavior: smooth;
}

.card {
  min-width: 250px;
  margin-right: 15px;
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 0 8px rgba(0,0,0,0.1);
}

.card-image {
  width: 100%;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}

.card-content {
  padding: 10px;
}

.meal-title {
  font-size: 16px;
  margin: 5px 0;
}

.meal-desc {
  font-size: 14px;
  color: #555;
}

.slide-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 30px;
  background: none;
  border: none;
  cursor: pointer;
  z-index: 1;
}

.slide-button.left {
  left: 0;
}

.slide-button.right {
  right: 0;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.4);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  background: white;
  padding: 30px;
  border-radius: 12px;
  width: 300px;
  text-align: center;
}

.modal-close {
  position: absolute;
  top: 10px;
  right: 15px;
  font-size: 20px;
  background: none;
  border: none;
  cursor: pointer;
}

.modal-title {
  font-size: 20px;
  margin-bottom: 10px;
}

.modal-body {
  font-size: 14px;
  margin-bottom: 20px;
}

.modal-confirm {
  padding: 8px 16px;
  background-color: #3b82f6;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}
</style>
