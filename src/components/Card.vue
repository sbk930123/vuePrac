<template>
  <div>
    <img class="room-img" :src="oneroomitem.image">
    <!-- <h4 @click="isModalOpen = true; matchId = a.id">{{ a.title }}</h4> -->
    <h4 @click="send()">{{  oneroomitem.title }}</h4>
    <p>{{ oneroomitem.price }} 원</p>
  </div>
</template>

<script>
export default {
  name : 'CardItem',
  props : {
    oneroomitem : Object,
    matchId : Number,
    isModalOpen : Boolean,
  },
  methods : {
    send() {
      this.$emit('openModal', this.oneroomitem.id);
    }
  }
}
</script>

<style>

</style>