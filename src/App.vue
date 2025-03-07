<script setup>
import {ref} from 'vue';
import rooms from '@/rooms.js'

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
  <div class="black-bg" v-if="isModalOpen">
    <div class="white-bg">
      <img :src="rooms[selectedIndex].image" style="width:300px">
      <h4> {{ rooms[selectedIndex].title }} </h4>
      <p> {{ rooms[selectedIndex].content }} </p>
      <button @click="closeModal">닫기</button>
    </div>
  </div>

  <div class="menu">
    <a v-for="menu in menus" :key="menu">
      {{ menu }}
    </a>
  </div>

  <div v-for="(room,i) in rooms" :key="i" class="room-container">
    <img :src="room.image" style="width:500px">
    <h4 @click="openModal(i)"> {{ room.title }} </h4>
    <p> {{ room.price }} </p>
    <p> {{ room.content }} </p>
  </div>
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

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.white-bg {
  width: 600px;
  background: white;
  border-radius: 8px;
  padding: 20px;
  text-align: center;
}

button {
  margin-top: 10px;
  padding: 5px 10px;
  cursor: pointer;
}
</style>