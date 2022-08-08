<template>

    <!-- 모달창 -->
    <!-- 
      0. 기본으로 만들어 놓음 (모달창)
      1. UI의 현재 상태를 데이터로 저장해둠 -> isModal: true or 1 / false or 0
      2. 데이터에 따라 UI가 어떻게 보일지 작성 -> false면 안보이고 true면 보이고 -> v- if
     -->

  <div class="black-bg" v-if="isModal == true">
      <div class="white-bg">
          <img :src="roomList[clickNumber].image" class="room-img"/>
          <h4>{{ roomList[clickNumber].title }}</h4>
          <p>{{ roomList[clickNumber].content }}</p>
          <input v-model.number="month" />
          <p>{{ month }}개월 선택함</p>
          <p>금액: {{ roomList[clickNumber].price * month }}만원</p>
          <DiscountPage />
          <button @click="$emit('closeModal')">닫기</button>
      </div>
    </div>

</template>

<script>
import DiscountPage from './DiscountPage.vue';

export default {
    name: 'ModalPage',
    data() {
        return {
            month: 1
        }
    },
    watch: {
        month(input) {
            
            // 사용자 입력값이 13보다 크면 경고문 띄우기
            if(input >= 13) {
                alert('13개월 이상은 불가능합니다.')
                this.month = 1
            }
            
            // 사용자 입력값이 number가 아닐 경우 경고문 띄우기
            if(typeof input !== 'number') {
                alert('숫자만 입력이 가능합니다.')
                this.month = 1
            }
        }
    },
    props: {
        roomList: Array,
        isModal: Boolean,
        clickNumber: Number,
    },
    components: { DiscountPage }
}
</script>

<style>

</style>