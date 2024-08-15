<template>
  <div>
    <div v-if="timeLeft > 0">
      <p>倒计时: {{ formattedTime }}</p>
    </div>
    <div v-else>
      <p style="color: #ff0000">时间到！请联系淘宝客服</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue';

const props = defineProps({
  initialTime: {
    type: Number,
    required: true
  }
});

const timeLeft = ref(props.initialTime);

const formattedTime = computed(() => {
  const minutes = Math.floor(timeLeft.value / 60);
  const seconds = timeLeft.value % 60;
  return `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
});

let timerId = null;

const updateTime = () => {
  if (timeLeft.value > 0) {
    timeLeft.value -= 1;
  } else {
    clearInterval(timerId);
  }
};

onMounted(() => {
  timerId = setInterval(updateTime, 1000);
});

onUnmounted(() => {
  clearInterval(timerId);
});
</script>

<style scoped>

</style>