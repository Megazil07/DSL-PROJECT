<script setup>
import { ref } from "vue";

// สถานะสำหรับแสดงหรือซ่อน Card
const showCard = ref(false);
const showConfirmationCard = ref(false); // ใช้สำหรับแสดง Card ที่ยืนยัน
const userInput = ref(""); // เก็บข้อความที่ผู้ใช้พิมพ์

function handleBack() {
  console.log("ย้อนกลับ");
  // เพิ่มการทำงานเมื่อกดปุ่มย้อนกลับ
}

function handlePauseSystem() {
  showCard.value = true; // แสดง Card
}

function handleCloseCard() {
  showCard.value = false; // ซ่อน Card
  userInput.value = ""; // ล้างข้อความที่ผู้ใช้พิมพ์
}

function handleSubmit() {
  if (!userInput.value.trim()) {
    alert("กรุณากรอกข้อมูลก่อนยืนยัน");
    return; // หยุดการทำงานหากไม่มีการกรอกข้อมูล
  }

  // แสดงการยืนยัน
  showConfirmationCard.value = true;
}

function handleCloseConfirmationCard() {
  showConfirmationCard.value = false;
  handleCloseCard(); // ซ่อน Card หลังจากกดยกเลิก
}
</script>

<template>
  <div class="relative w-screen  bg-gray-100 p-4">
    <!-- ปุ่มย้อนกลับ -->
    <button
      @click="handleBack"
      class="bg-gray-300 text-black px-10 py-5 rounded-md hover:bg-gray-400"
    >
      ย้อนกลับ
    </button>

    <!-- ปุ่มพักระบบ -->
    <button
      @click="handlePauseSystem"
      class="bg-yellow-500 text-black px-10 py-5 rounded-md font-semibold hover:bg-yellow-600 ml-4"
    >
      พักระบบ
    </button>

    <!-- Card สำหรับกรอกข้อความ -->
    <div
      v-if="showCard"
      class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50"
    >
      <div class="bg-white rounded-lg shadow-lg p-6 w-96">
        <h3 class="text-xl font-bold mb-4">ระบุหัวข้อในการพักระบบพร้อมระบุเวลาที่จะมาเปิดอีกครั้ง</h3>
        
        <!-- ช่องให้ผู้ใช้พิมพ์ -->
        <textarea
          v-model="userInput"
          rows="4"
          class="w-full p-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-yellow-500"
          placeholder="เช่น เจ้าหน้าที่กำลังพักกลางวัน จะกลับมาให้บริการอีกครั้ง 13.30 pm"
        ></textarea>

        <!-- ปุ่มใน Card -->
        <div class="flex justify-end mt-4">
          <button
            @click="handleCloseCard"
            class="bg-gray-300 text-black px-4 py-2 rounded-md hover:bg-gray-400 mr-2"
          >
            ยกเลิก
          </button>
          <button
            @click="handleSubmit"
            class="bg-green-500 text-black px-4 py-2 rounded-md font-semibold hover:bg-yellow-600"
          >
            ยืนยัน
          </button>
        </div>
      </div>
    </div>

    <!-- Card สำหรับการยืนยัน -->
    <div
      v-if="showConfirmationCard"
      class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50"
    >
      <div class="bg-white rounded-lg shadow-lg p-6 w-96">
        <h3 class="text-xl font-bold mb-4">กำลังพักระบบในเรื่อง....</h3>
        <p class="mb-4">{{ userInput }}</p>
        <div class="flex justify-end">
          <button
            @click="handleCloseConfirmationCard"
            class="bg-red-600 text-black px-4 py-2 rounded-md hover:bg-gray-400 mr-2"
          >
            ยกเลิกพักระบบ
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
