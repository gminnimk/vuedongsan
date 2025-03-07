<script setup>
import {ref} from 'vue';

const menus = ['Home', 'Shop', 'About'];

const oneRooms = [
  {title: '서울특별시', price: '60만원', reportCount: ref(0)},
  {title: '강원특별자치도', price: '60만원', reportCount: ref(0)},
  {title: '부산광역시', price: '60만원', reportCount: ref(0)}
]

const increase = (i) => {
  oneRooms[i].reportCount.value += 1;
}

</script>

<template>

  <div class="menu">
    <a v-for="menu in menus" :key="menu">
      {{ menu }}
    </a>
  </div>

  <div v-for="(room,i) in oneRooms" :key="i" class="room-container">
    <h4>{{ room.title }}</h4>
    <p> {{ room.price }}</p>
    <button @click="increase(i)">허위매물신고</button>
    <span>신고수 : {{ room.reportCount }}</span>
  </div>

</template>

<style scoped>
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
</style>