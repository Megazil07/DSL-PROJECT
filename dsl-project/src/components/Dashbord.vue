<script setup>
import { ref, onMounted } from 'vue';

const totalReservations = ref(0);
const inQueue = ref(0);
const completed = ref(0);
const skipped = ref(0);

// ฟังก์ชันจำลองการดึงข้อมูลจากฐานข้อมูล
async function fetchData() {
  // จำลองข้อมูลที่มาจาก API หรือฐานข้อมูล
  const data = await new Promise((resolve) => {
    setTimeout(() => {
      resolve({
        totalReservations: 300,
        inQueue: 80,
        completed: 70,
        skipped: 5,
      });
    }, 1000); 
  });

  // อัปเดตตัวแปรด้วยข้อมูลที่ได้
  totalReservations.value = data.totalReservations;
  inQueue.value = data.inQueue;
  completed.value = data.completed;
  skipped.value = data.skipped;
}

// เรียก fetchData เมื่อ component ถูก mount
onMounted(() => {
  fetchData();
});
</script>

<template>
  <div class="bg-blue-900 text-white font-sans w-full h-[300px] mx-auto py-10 px-4 flex items-center justify-center">
    <div class="max-w-screen-lg mx-auto py-10">
      <h1 class="text-lg font-bold mb-6">DASHBORD</h1>
      <div class="grid grid-cols-4 gap-4">
        <div class="text-center">
          <p class="text-6xl font-bold">{{ totalReservations }}</p>
          <p class="text-lg mt-2">จำนวนการจองคิววันนี้</p>
        </div>
        <div class="text-center">
          <p class="text-6xl font-bold">{{ inQueue }}</p>
          <p class="text-lg mt-2">อยู่ในคิว</p>
        </div>
        <div class="text-center">
          <p class="text-6xl font-bold">{{ completed }}</p>
          <p class="text-lg mt-2">คิวสำเร็จ</p>
        </div>
        <div class="text-center">
          <p class="text-6xl font-bold">{{ skipped }}</p>
          <p class="text-lg mt-2">คิวที่ข้าม</p>
        </div>
      </div>
    </div>
  </div>
</template>
