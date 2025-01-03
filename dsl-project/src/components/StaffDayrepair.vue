<template>
    <div class="flex flex-col items-center justify-center p-6 space-y-4 mt-40">
      <div class="flex space-x-4">
        <h1 v-for="day in visibleDays" :key="day" :class="['text-7xl font-bold', days[day]]">
          {{ day }}
        </h1>
      </div>
      <p class="text-6xl font-bold">เปิดรับเฉพาะเอกสารแก้ไข</p>
      <button @click="toggleDropdown" class="bg-indigo-600 text-white px-6 py-3 rounded shadow hover:bg-indigo-500 focus:outline-none focus:ring-2 focus:ring-indigo-400 mt-10">
        เปลี่ยนวันที่ส่งเอกสารแก้ไข
      </button>
      <div v-if="dropdownVisible" class="mt-4 w-64 bg-white border rounded shadow-md p-4 space-y-2">
        <label v-for="(color, day) in days" :key="day" class="flex items-center space-x-2">
          <input type="checkbox" v-model="selectedDays" :value="day" class="form-checkbox h-5 w-5 text-indigo-600" />
          <span :class="color">{{ day }}</span>
        </label>
        <button @click="confirmSelection" class="mt-4 bg-green-600 text-white px-6 py-3 rounded shadow hover:bg-green-500 focus:outline-none focus:ring-2 focus:ring-green-400">
          ยืนยัน
        </button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        days: {
          "จันทร์": "text-yellow-500 ",
          "อังคาร": "text-pink-500",
          "พุธ": "text-green-500",
          "พฤหัสบดี": "text-orange-500",
          "ศุกร์": "text-blue-500",
          "เสาร์": "text-purple-500",
          "อาทิตย์": "text-red-500",
        },
        selectedDays: ["ศุกร์"],
        visibleDays: ["ศุกร์"],
        dropdownVisible: false,
      };
    },
    methods: {
      toggleDropdown() {
        this.dropdownVisible = !this.dropdownVisible;
      },
      confirmSelection() {
        this.visibleDays = [...this.selectedDays];
        this.dropdownVisible = false;
      },
    },
  };
  </script>
  

  