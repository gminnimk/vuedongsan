<script setup>
import {defineProps, defineEmits} from 'vue';

defineProps({
  rooms: ({
    type: Array,
    required: true
  }),
  isModalOpen: ({
    type: Boolean,
    required: true
  }),
  selectedIndex: ({
    type: Number,
    required: true
  })
})

// 자식은 데이터 변환이 불가능, 오로지 받기만 가능
// 변환을 하기 위한 방법은 => emit 사용하여 부모에게 요청

const emit = defineEmits(['closeModal']);

const closeModal = () => {
  emit('closeModal');
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
</template>

<style scoped>
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

</style>