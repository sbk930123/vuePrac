<template>
  <div class="black-bg" v-if="isModalOpen">
    <div class="white-bg">
      <h4>{{ oneroom[matchId].title }}</h4>
      <img class="room-img" :src="oneroom[matchId].image">
      <p>{{ oneroom[matchId].content }}</p>
      <input v-model.number="month">
      <p> {{ month }} 개월 선택함 {{ oneroom[matchId].price * month }} 원 </p>
      <button @click="send()">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name : 'ModalWindow',

  data() {
    return {
      month : 1,
    }
  },

  beforeUpdate() {
    if(this.month == 2) {
      alert('2개월은 너무 짧아 결제가 불가능합니다.')
      this.month = 1;
    }
  },

  watch : {
    month(a) {
      if(isNaN(a) == true) {
        alert('숫자만 입력이 가능합니다.');
        this.month = 1;
      } else if(a < 0 || a > 12) {
        alert('숫자는 0~12까지 입력 가능합니다.');
        this.month = 1;
      } 
    },
  },

  props : {
    oneroom : Array,
    matchId : Number,
    isModalOpen : Boolean,
  },
  methods : {
    send() {
      this.$emit('closeModal');
    }
  }
}
</script>

<style>

</style>