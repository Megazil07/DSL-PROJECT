<script setup>
import { ref, onMounted } from "vue";

const currentDateTime = ref("");

const updateDateTime = () => {
  const now = new Date();
  const options = { 
    year: "numeric", 
    month: "long", 
    day: "numeric", 
    hour: "2-digit", 
    minute: "2-digit" 
  };
  currentDateTime.value = now.toLocaleDateString("th-TH", options); // แสดงผลในรูปแบบไทยโดยไม่มีวินาที
};

onMounted(() => {
  updateDateTime();
  setInterval(updateDateTime, 60000); // อัปเดตทุก 1 นาที (แทน 1 วินาที)
});
</script>

<template>
  <nav class="bg-white shadow-md h-[100px]">
    <div class="container max-w-7xl px-4 py-2 mt-5">
      <div class="flex justify-between items-center">
        <!-- Left side: Logo and Text -->
        <div class="flex items-center space-x-4">
          <img src="/src/assets/img/logo.jpg" alt="Logo" class="h-20"> 
          <div>
            <p class="text-black lg:text-2xl font-bold">MFU DSL EQUEUE</p>
            <p class="text-black text-sm lg:text-md font-bold">ระบบจองคิว กยศ มหาวิทยาลัยแม่ฟ้าหลวง</p>
          </div>
        </div>
        <!-- Right side: Current Date and Time -->
        <div class="bg-gray-200 text-black font-semibold text-lg px-4 py-2 rounded-md shadow-md h-[60px] text-5xl">
          {{ currentDateTime }}<span> น. </span>
        </div>
      </div>
    </div>
  </nav>
</template>
