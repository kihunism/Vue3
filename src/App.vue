<template>

  <div>
    <DiscountPage v-if="showDiscountPage" />

    <button @click="priceSortUp">가격순 정렬 (오름차순)</button>
    <button @click="priceSortDown">가격순 정렬 (내림차순)</button>
    <button @click="backSort">정렬 초기화</button>
    <transition name="fade">
      <ModalPage @closeModal="setIsModal()" :roomList="roomList" :isModal="isModal" :clickNumber="clickNumber" />
    </transition>
    <div class="menu">
      <a v-for="(i, key) in menus" :key="key">{{ i }}</a>
    </div>
    <ListCard @openModal="setIsModal(i)" v-for="(room, i) in roomList" :key="i" :room="roomList[i]" />
  </div>
</template>

<script>

import roomList from './assets/data'
import ModalPage from './ModalPage.vue'
import ListCard from './ListCard.vue'
import DiscountPage from './DiscountPage.vue'

export default {
  name: 'App',
  data() {
    return {
      showDiscountPage: true,
      clickNumber: 0,
      roomList: roomList,
      originalRoomList: [...roomList], // 복사본
      isModal: false,
      price1: 80,
      price2: 100,
      price3: 150,
      logo: '로고샵',
      style: 'color: blue',
      products: ['역삼동 원룸', '천호동 원룸', '마포구원룸'],
      prices: ['80만원', '100만원', '150만원'],
      menus: ['Home', 'Products', 'About'],
      reports: [0, 0, 0]
    }
  },
  methods: {
    increase(key) {
      // 함수 생성
      this.reports[key]++
    },
    reset(key) {
      this.reports[key] = 0
    },
    setIsModal(i) {
      this.isModal = !this.isModal
      this.clickNumber = i
    },
    priceSortUp() {
      this.roomList.sort((a, b) => {
        return a.price - b.price
      })
    },
    priceSortDown() {
      this.roomList.sort((a, b) => {
        return b.price - a.price
      })
    },
    backSort() {
      this.roomList = [...this.originalRoomList]
    },
  },

  beforeMount() {
    
    // 마운트되기 전
  },

  mounted() {
  
    // 라이프사이클 훅 (Hook) -> 마운트되고 나서!
    
  },

  components: {
    ModalPage,
    ListCard,
    DiscountPage
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 30%;
  margin-top: 40px;
}

body {
  margin: 0
}

div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}

.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

.discount {
  background: gray;
  padding: 20px;
  margin: 10px;
  border-radius: 5px;
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

.fade-enter-from {
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  transform: translateY(0px);
}
</style>
