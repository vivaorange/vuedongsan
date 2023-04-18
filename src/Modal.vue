<template>
  <div class="blackBg" v-if="modalState == true">
    <div class="whiteBg">
      <img :src="oneRooms[clickBtn].image" class="roomImg" />
      <h4>{{ oneRooms[clickBtn].title }}</h4>
      <p>{{ oneRooms[clickBtn].content }}</p>
      <!-- <input @input="month = $event.target.value" /> -->
      <input v-model.number="month" />
      <p>{{ month }}개월 선택함 : {{ oneRooms[clickBtn].price * month }} 원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      month: 1,
    };
  },
  watch: {
    month(a) {
      if (isNaN(a) === true) {
        alert("숫자가 아닙니다.\n\n0-9의 정수만 허용합니다.");
        this.month = 1;
      }
    },
  },
  beforeUpdate() {
    if (this.month === 2) {
      alert("2는 입력못함");
      this.month = 3;
    }
  },
  props: {
    oneRooms: Array,
    clickBtn: Number,
    modalState: Boolean,
  },
};
</script>

<style></style>
