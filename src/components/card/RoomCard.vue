<script setup>
import {defineProps, defineEmits} from 'vue';

defineProps({
  rooms: {
    type: Array,
    required: true
  },
  isModalOpen: {
    type: Boolean,
    required: true
  },
  selectedIndex: {
    type: Number,
    required: true
  }
})

const emit = defineEmits(['openModal']);

const openModal = (i) => {
  emit('openModal',i)
}

</script>

<template>
  <div v-for="(room,i) in rooms" :key="i" class="room-container">
    <img :src="room.image" style="width:500px">
    <h4 @click="openModal(i)"> {{ room.title }} </h4>
    <p> {{ room.price }} </p>
    <p> {{ room.content }} </p>
  </div>
</template>

<style scoped>

</style>