<template>
  <transition name="fade">
    <Modal
      @closeModal="modalState = false"
      :oneRooms="oneRooms"
      :clickBtn="clickBtn"
      :modalState="modalState"
    />
  </transition>
  <div class="menu">
    <a v-for="(menu, i) in menus" :key="i">{{ menu }}</a>
  </div>

  <Discount v-if="showDiscount === true" />

  <button @click="priceSortLow">가격낮은순</button>
  <button @click="priceSortHigh">가격높은순</button>
  <button @click="titleSortLow">내림차순</button>
  <button @click="titleSortHigh">오름차순</button>
  <button @click="priceOver">50만원 이하</button>
  <button @click="sortBack">되돌리기</button>

  <Card
    @openModal="
      modalState = true;
      clickBtn = $event;
    "
    :oneRoom="oneRooms[i]"
    v-for="(oneRoom, i) in oneRooms"
    :key="i"
  />
</template>

<script>
import data from "./assets/data/oneRoom.js";
import Discount from "./Discount.vue";
import Modal from "./Modal.vue";
import Card from "./Card.vue";

export default {
  name: "App",
  data() {
    return {
      showDiscount: true,
      oneRoomsOriginal: [...data],
      clickBtn: 0,
      oneRooms: data,
      modalState: false,
      report: [0, 0, 0],
      menus: ["Home", "Shop", "About"],
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
    };
  },
  methods: {
    increase(i) {
      this.report[i]++;
    },
    sortBack() {
      this.oneRooms = [...this.oneRoomsOriginal];
    },
    priceSortLow() {
      this.oneRooms.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    priceSortHigh() {
      this.oneRooms.sort(function (a, b) {
        return b.price - a.price;
      });
    },
    titleSortLow() {
      this.oneRooms.sort(function (a, b) {
        return a.title < b.title ? -1 : a.title > b.title ? 1 : 0;
      });
    },
    titleSortHigh() {
      this.oneRooms.sort(function (a, b) {
        return b.title < a.title ? -1 : b.title > a.title ? 1 : 0;
      });
    },
    priceOver() {
      let overPrice = this.oneRooms.filter(function (a) {
        console.log(a.price);
        return a.price < 500000;
      });
      this.oneRooms = overPrice;
    },
  },

  mounted() {
    // setTimeout(() => {
    //   this.showDiscount = false;
    // }, 2000);
  },

  components: {
    Discount: Discount,
    Modal: Modal,
    Card: Card,
  },
};
</script>

<style>
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 0.5s;
}
.fade-leave-to {
  opacity: 0;
}
.fade-enter-from {
  opacity: 0;
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 0.5s;
}
.fade-enter-to {
  opacity: 1;
  transform: translateY(0px);
}
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

.blackBg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.whiteBg {
  width: 100%;
  background: white;
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
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}

.roomImg {
  width: 100%;
  margin-top: 40px;
}
</style>
