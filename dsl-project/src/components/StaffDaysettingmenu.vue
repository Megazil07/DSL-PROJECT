<script setup>
import { reactive } from 'vue';

const item = reactive({
  option_1: {
    title: 'แบบคำขอกู้ยืม',
    image: '/src/assets/img/option_1.jpg',
    link: '/StaffCallQueue' //ไปหน้าไหนมากำหนดตรงนี้
  },
  option_2: {
    title: 'สัญญากู้ยืม และ แบบเบิกเงินกู้ยืม',
    image: '/src/assets/img/option_2.jpg',
    link: '/page2' //ไปหน้าไหนมากำหนดตรงนี้
  },
  option_3: {
    title: 'เปลี่ยนแปลงวันที่สำหรับส่งเอกสารแก้ไข',
    image: '/src/assets/img/option_3.jpg', 
    link: '/page3' //ไปหน้าไหนมากำหนดตรงนี้
  },
});
</script>

<template>
    <p class="text-center mt-20 mb-10 text-8xl font-bold">ตั้งค่าวันที่</p>
  <section class="py-10 mb-4">
    <div class="container mx-auto px-4">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <!-- Card Loop -->
        <router-link
          v-for="(option, index) in item"
          :key="index"
          :to="option.link"
          class="relative overflow-hidden rounded-lg shadow-lg group"
        >
          <!-- Image -->
          <img
            :src="option.image"
            alt="Option Image"
            class="w-full h-48 object-cover group-hover:scale-105 transition-transform duration-300"
          />

          <!-- Dark Overlay -->
          <div class="absolute inset-0 bg-black opacity-70"></div>

          <!-- Text Content -->
          <div class="absolute inset-0 p-4 text-white flex flex-col items-center justify-center">
            <!-- Icon -->
            <i :class="option.icon" class="text-4xl mb-4"></i> <!-- Font Awesome Icon -->

            <!-- Title -->
            <h3 class="text-3xl font-bold mb-2 text-center">{{ option.title }} </h3> <!-- Increased text size -->
          </div>
        </router-link>
      </div>
    </div>
  </section>
</template>

