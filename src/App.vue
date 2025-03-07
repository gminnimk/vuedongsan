<script setup>
import {ref} from 'vue';
import rooms from '@/rooms.js'
import DiscountBanner from "@/components/banner/DiscountBanner.vue";
import RoomModal from "@/components/modal/RoomModal.vue";
import RoomCard from "@/components/card/RoomCard.vue";

const menus = ['Home', 'Shop', 'About'];

const isModalOpen = ref(false);

const selectedIndex = ref(0); // 선택된 원룸의 번호를 저장 할 변수s

const openModal = (i) => {
  selectedIndex.value = i;
  isModalOpen.value = true;
}

const closeModal = () => {
  isModalOpen.value = false;
}

</script>

<template>

  <RoomModal
      :rooms="rooms"
      :isModalOpen="isModalOpen"
      :selected-index="selectedIndex"
      @closeModal="closeModal"
  />

  <div class="menu">
    <a v-for="menu in menus" :key="menu">
      {{ menu }}
    </a>
  </div>
  <RoomCard
      :rooms="rooms"
      :isModalOpen="isModalOpen"
      :selected-index="selectedIndex"
      @openModal="openModal"
  />

  <DiscountBanner/>

</template>

<style scoped>
body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
  text-align: center;
}

.menu a {
  color: white;
  padding: 10px;
}

.room-container {
  text-align: center;
}

button {
  margin-top: 10px;
  padding: 5px 10px;
  cursor: pointer;
}
</style>