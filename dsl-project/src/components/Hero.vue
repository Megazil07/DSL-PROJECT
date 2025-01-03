<script setup>
import { defineProps } from 'vue';

defineProps({
  title:{
    type:String,
    default: 'Become a Vue Day'
  },subtitle:{
    type:String,
    default: 'Find the Vue job that fits your skills and needs'
  }
})
</script>

<template>
    <section class="bg-indigo-900 py-10 lg:py-20 mb-4">
      <div class="grid grid-cols-2 gap-3 content-between p-3">
        <div class="relative overflow-hidden rounded-3xl shadow-xl group m-3">
          <img 
          src="/src/assets/img/logo_2.jpg" 
            alt="Contract Reservation" 
            class="w-full h-full object-cover = group-hover:scale-105 transition-transform duration-300"
          />

        </div>

        <div class="text-white">
          <h1 class="font-bold text-sm md:text-lg lg:text-4xl mb-3">MFU DSL EQUEUE คืออะไร</h1>
          <p class="text-sm md:text-md lg:text-2xl">มหาวิทยาลัยแม่ฟ้าหลวง ขอแนะนำระบบจองคิว กยศ. ออนไลน์ที่ทันสมัยช่วยให้นักศึกษาสามารถจองคิวเพื่อขอรับบริการด้านการกู้ยืมเงิน กยศ.ได้ง่ายๆ เพียงแค่ไม่กี่คลิก ประหยัดเวลาและลดความยุ่งยากในการเดินทางมาที่สำนักงาน ไม่ต้องเสียเวลารอคิวอีกต่อไป เพียงแค่ทำการจองคิวล่วงหน้า ก็สามารถเข้ารับบริการได้ตามวันและเวลาที่กำหนด</p>
        </div>
  
      </div>
    </section>
</template>