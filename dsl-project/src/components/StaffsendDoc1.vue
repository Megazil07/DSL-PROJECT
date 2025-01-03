<template>
    <p class="text-4xl font-bold mt-8 text-center">ตั้งค่าช่วงวันที่</p>
    <p class="text-5xl font-bold mt-8 text-center">แบบคำขอกู้ยืม</p>
  
    <div class="flex justify-center mt-12">
      <button class="bg-orange-500 text-white font-bold text-3xl py-4 px-6 rounded-lg shadow-lg hover:bg-orange-600 mr-4" @click="addSpecialRound">
        เพิ่มรอบเก็บตก
      </button>
      <button 
        class="bg-blue-500 text-white font-bold text-3xl py-4 px-6 rounded-lg shadow-lg hover:bg-blue-600"
        @click="addCard"
      >
        เพิ่มช่วงวัน
      </button>
    </div>
  
    <div class="flex flex-wrap justify-center gap-6 mt-8">
      <div class="bg-gray-100 p-6 rounded-lg shadow-xl flex flex-col items-center w-72" v-for="(card, index) in cards" :key="card.id">
        <p class="text-xl font-bold mb-4 text-center">{{ card.title }}</p>
        <p v-if="card.title !== 'รอบเก็บตก'" class="text-2xl font-bold text-center">1-15</p>
        <p v-if="card.title !== 'รอบเก็บตก'" class="text-2xl font-bold text-center">สิงหาคม</p>
        <p v-if="card.title !== 'รอบเก็บตก'" class="text-2xl font-bold text-center">2567</p>
        <div class="flex flex-col mt-4 space-y-2 w-full">
          <button 
            class="bg-blue-500 text-white font-bold text-base py-2 rounded-lg shadow-lg hover:bg-blue-600"
            @click="selectDateRange(index)"
          >
            เลือกช่วงวัน
          </button>
          <button 
            class="bg-red-500 text-white font-bold text-base py-2 rounded-lg shadow-lg hover:bg-red-600"
            @click="confirmRemoveCard(index)"
          >
            ลบช่วงวัน
          </button>
        </div>
      </div>
    </div>
  
    <!-- Confirmation alert card -->
    <div v-if="isConfirming" class="fixed inset-0 flex justify-center items-center bg-gray-500 bg-opacity-50">
      <div class="bg-white p-6 rounded-lg shadow-lg w-96">
        <p class="text-xl font-bold mb-4 text-center">คุณแน่ใจหรือไม่ว่าต้องการ ลบ ช่วงวันนี้?</p>
        <div class="flex justify-center gap-6">
          <button 
            class="bg-red-500 text-white font-bold py-2 px-6 rounded-lg shadow-lg hover:bg-green-600"
            @click="removeCard"
          >
            ยืนยัน
          </button>
          <button 
            class="bg-gray-500 text-white font-bold py-2 px-6 rounded-lg shadow-lg hover:bg-gray-600"
            @click="cancelRemoveCard"
          >
            ยกเลิก
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "DateSettingButtons",
    data() {
      return {
        cards: [],
        isConfirming: false,
        cardToRemoveIndex: null,
      };
    },
    methods: {
      addCard() {
        this.cards.push({ id: Date.now(), title: `รอบที่ ${this.cards.length + 1} ระหว่างวันที่` });
      },
      addSpecialRound() {
        this.cards.push({ id: Date.now(), title: "รอบเก็บตก" });
      },
      confirmRemoveCard(index) {
        this.isConfirming = true;
        this.cardToRemoveIndex = index;
      },
      removeCard() {
        if (this.cardToRemoveIndex !== null) {
          this.cards.splice(this.cardToRemoveIndex, 1);
          this.isConfirming = false;
          this.cardToRemoveIndex = null;
        }
      },
      cancelRemoveCard() {
        this.isConfirming = false;
        this.cardToRemoveIndex = null;
      },
      selectDateRange(index) {
        alert(`เลือกช่วงวันสำหรับรอบที่ ${index + 1}`);
      },
    },
  };
  </script>
  
  <style scoped>
  .flex-wrap {
    display: flex;
    flex-wrap: wrap;
  }
  </style>
  