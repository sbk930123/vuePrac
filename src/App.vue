<template>

  <transition name="fade">
    <ModalWindow @closeModal="isModalOpen = false;" :oneroom="oneroom" :matchId="matchId" :isModalOpen="isModalOpen" />
  </transition>

  <div class="menu">
    <a v-for="(a, i) in menus" :key="i"> {{ a }} </a>
  </div>

  <DiscountOffer :discountPercent="discountPercent" v-if="showDiscount" />

  <button @click="priceSort()">가격낮은순정렬</button>
  <button @click="priceReverseSort()">가격높은순정렬</button>
  <button @click="titleSort()">상품명 가나다순정렬</button>
  <button @click="sortBack()">원상태 정렬</button>

  <CardItem @openModal="isModalOpen = true; matchId = $event;" :oneroomitem="oneroom[i]" v-for="(a, i) in oneroom" :key="i"/>
  
</template>


<!-- script -->


<script>

import data from './assets/oneroom.js';
import DiscountOffer from './components/Discount.vue';
import ModalWindow from './components/Modal.vue';
import CardItem from './components/Card.vue';

export default {
  name: 'App',
  data() {
    return {
      discountPercent: 30,
      showDiscount: true,
      oneroomBackUp: [...data],
      matchId: 0,
      oneroom: data,
      isModalOpen: false,
      menus: ['Home', 'Shop', 'About'],
      products: ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },

  methods: {
    priceSort() {
      this.oneroom.sort(function(a, b) {
        return a.price - b.price
      });
    },

    priceReverseSort() {
      this.oneroom.sort(function(a, b) {
        return b.price - a.price
      })
    },

    titleSort() {
      this.oneroom.sort(function(a, b) {
        return a.title > b.title ? 1 : -1
      })
    },

    sortBack() {
      this.oneroom = [...this.oneroomBackUp];
    }
  },

  mounted() {
    setInterval(() => {
      this.discountPercent--
    }, 1000);
  },

  components: {
    CardItem : CardItem,
    ModalWindow : ModalWindow,
    DiscountOffer : DiscountOffer,
  }
}
</script>


<!-- style -->


<style>
body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.fade-leave-from {opacity: 1;}
.fade-leave-active {transition: opacity 1s;}
.fade-leave-to {opacity: 0;}

.fade-enter-from {transform: translateY(-1000px);}
.fade-enter-active {transition: transform 1s;}
.fade-enter-to {transform: translateY(0);}

.black-bg {
  width: 100%;
  height: 100%;
  background-color: rgb(0, 0, 0, .5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background-color: white;
  border-radius: 8px;
  padding: 20px;
}


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background-color: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.discount {
  background-color: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}
</style>
