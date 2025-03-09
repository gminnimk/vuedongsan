<script setup>
import {onMounted, ref} from 'vue';
import roomsData from '@/rooms.js'
import DiscountBanner from "@/components/banner/DiscountBanner.vue";
import RoomModal from "@/components/modal/RoomModal.vue";
import RoomCard from "@/components/card/RoomCard.vue";

const menus = ['Home', 'Shop', 'About'];

const rooms = ref([...roomsData]);
const originalRooms = [...roomsData];

const isModalOpen = ref(false);

const selectedIndex = ref(0); // 선택된 원룸의 번호를 저장 할 변수s

const openModal = (i) => {
  selectedIndex.value = i;
  isModalOpen.value = true;
}

const closeModal = () => {
  isModalOpen.value = false;
}

const priceSort = () => {
  rooms.value.sort((a, b) => {
    return a.price - b.price;
  })
}

const sortBack = () => {
  rooms.value = [...originalRooms];
}

const showDiscount = ref(true);

onMounted(() => {
  setTimeout(() => {
    showDiscount.value = false
  }, 2000);
});

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
  <DiscountBanner v-if="showDiscount" />

  <div class="btn-container">
    <button @click="priceSort">가격 순 정렬</button>
    <button @click="sortBack">되돌리기</button>
  </div>
  <RoomCard
      :rooms="rooms"
      :isModalOpen="isModalOpen"
      :selected-index="selectedIndex"
      @openModal="openModal"
  />

</template>

<style scoped>
body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.menu {
  height: 70px;
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
  text-align: center;
  transform: translateY(-50px);
}

.menu:hover {
  transform: translateY(2px);
  transition-duration: 0.3s;
}

.menu a {
  color: white;
  padding: 10px;
  font-size: 20px;
}

.btn-container {
  text-align: center;
  margin: 30px;

  button {
    margin: 10px;
    background-color: darkcyan;
    border-radius: 5px;
    color: white;
  }

  button:hover {
    transform: translateY(5px);
    transition-duration: 0.2s;
  }
}

button {
  margin-top: 10px;
  padding: 5px 10px;
  cursor: pointer;
}
</style>