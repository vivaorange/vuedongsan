<template>
  <div class="discount">
    <h4>지금 결제하면 {{ amount }}% 할인</h4>
  </div>
</template>

<script>
export default {
  name: "Discount",
  data() {
    return {
      amount: 30,
    };
  },
  mounted() {
    setInterval(() => {
      if (this.amount > 0) {
        this.amount--;
      }
    }, 1000);
  },
};
</script>

<style></style>
