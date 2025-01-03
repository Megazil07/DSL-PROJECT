<template>
    <div class="text-center mt-20">
      <!-- ตัวอักษรที่สามารถเปลี่ยนค่าได้ -->
      <p class="font-bold text-6xl text-black animate-marquee">{{ dynamicText }}</p>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const dynamicText = ref('ระบบเปิดเรียกคิวปกติ')
  </script>
  
  <style scoped>
  /* Animation for left-to-right marquee */
  @keyframes marquee {
    0% {
      transform: translateX(-100%);
    }
    100% {
      transform: translateX(100%);
    }
  }
  
  .animate-marquee {
    display: inline-block;
    white-space: nowrap;
    animation: marquee 8s linear infinite; /* Adjust time for speed */
  }
  </style>
  