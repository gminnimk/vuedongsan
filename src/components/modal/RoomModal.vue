<script setup>
import {ref, watch} from 'vue';
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
// 변환을 하기 위한 방법은 => emit 사용하여 부모에게 요청(custom event)

const emit = defineEmits(['closeModal']);

const closeModal = () => {
  emit('closeModal');
}

const month = ref(1);

watch(month, (newValue) => {
  if (newValue >= 12) {
    alert("12 이하의 숫자만 입력해주세요!")
  } else if (isNaN(newValue)) {
    alert("숫자만 입력하세요!")
    month.value = 1;
  }
});

</script>

<template>
  <div class="black-bg" v-if="isModalOpen">
    <div class="white-bg">
      <img :src="rooms[selectedIndex].image" style="width:300px">
      <h4> {{ rooms[selectedIndex].title }} </h4>
      <p> {{ rooms[selectedIndex].content }} </p>

      <input v-model.number="month" placeholder="월 입력" class="month">
      <p>{{ month }}개월 선택함: {{ rooms[selectedIndex].price * month }}</p>
      <button @click="closeModal" class="close-btn">닫기</button>
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

.close-btn {
  display: block;
  margin: auto;
  margin-bottom: 20px;
}

</style>