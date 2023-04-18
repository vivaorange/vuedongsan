<template>
  <div>
    <img :src="oneRoom.image" class="roomImg" />
    <h4 @click="$emit('openModal', oneRoom.id)">
      {{ oneRoom.title }}
    </h4>
    <p>{{ oneRoom.price }}원</p>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    oneRoom: Array,
  },
};
</script>

<style></style>
