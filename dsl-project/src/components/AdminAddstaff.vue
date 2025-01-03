<script setup>
import { ref } from 'vue';

const staffs = ref([]);
const showAddCard = ref(false);
const showChangeCard = ref(false);
const showDeleteCard = ref(false);
const newEmail = ref('');
const selectedServiceNumber = ref(null);
const selectedStaffIndex = ref(null);
let serviceNumber = 1;

const openAddCard = () => {
    showAddCard.value = true;
};

const confirmAddStaff = () => {
    if (newEmail.value) {
        staffs.value.push({
            email: newEmail.value,
            serviceNumber: serviceNumber++
        });
        newEmail.value = '';
        showAddCard.value = false;
        alert('Staff added successfully!');
    }
};

const cancelAddStaff = () => {
    newEmail.value = '';
    showAddCard.value = false;
    alert('Staff addition cancelled.');
};

const openChangeServiceCard = (index) => {
    selectedStaffIndex.value = index;
    showChangeCard.value = true;
};

const confirmChangeService = () => {
    if (selectedServiceNumber.value) {
        staffs.value[selectedStaffIndex.value].serviceNumber = selectedServiceNumber.value;
        showChangeCard.value = false;
        alert('Service channel updated!');
    }
};

const cancelChangeService = () => {
    showChangeCard.value = false;
};

const openDeleteCard = (index) => {
    selectedStaffIndex.value = index;
    showDeleteCard.value = true;
};

const confirmDeleteStaff = () => {
    staffs.value.splice(selectedStaffIndex.value, 1);
    showDeleteCard.value = false;
    alert('Staff removed successfully.');
};

const cancelDelete = () => {
    showDeleteCard.value = false;
};
</script>

<template>
  <div class="p-6 text-center">
    <div class="mb-12">
      <button @click="openAddCard" class="bg-blue-500 text-white px-8 py-4 rounded text-xl hover:bg-blue-700">เพิ่ม Staff</button>
    </div>

    <div v-if="showAddCard" class="fixed inset-0 flex items-center justify-center bg-gray-500 bg-opacity-50">
      <div class="bg-white border border-gray-300 rounded-lg shadow-lg p-6 w-80 text-center">
        <h2 class="text-xl font-bold mb-4">Add New Staff</h2>
        <input v-model="newEmail" type="email" placeholder="Enter staff email" class="border border-gray-300 p-2 rounded w-full mb-4" />
        <div class="flex justify-around">
          <button @click="confirmAddStaff" class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700">เพิ่ม Staff</button>
          <button @click="cancelAddStaff" class="bg-gray-500 text-white px-4 py-2 rounded hover:bg-gray-700">ยกเลิก</button>
        </div>
      </div>
    </div>

    <div class="mt-8">
      <h2 class="text-3xl font-bold mb-4 text-red-500">STAFF</h2>
      <div v-for="(staff, index) in staffs" :key="index" class="inline-block m-4">
        <div class="border border-gray-300 rounded-lg shadow-lg p-6 w-64 text-center">
          <p class="text-lg font-medium">{{ staff.email }}</p>
          <p class="mt-2">ช่องบริการที่ : <strong>{{ staff.serviceNumber }}</strong></p>
          <div class="mt-4 flex justify-center space-x-4">
            <button @click="openDeleteCard(index)" class="bg-red-500 text-white px-4 py-2 rounded hover:bg-red-700">ลบ</button>
            <button @click="openChangeServiceCard(index)" class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700">เปลี่ยนช่องบริการ</button>
          </div>
        </div>
      </div>
    </div>

    <div v-if="showChangeCard" class="fixed inset-0 flex items-center justify-center bg-gray-500 bg-opacity-50">
      <div class="bg-white border border-gray-300 rounded-lg shadow-lg p-6 w-80 text-center">
        <h2 class="text-xl font-bold mb-4">เปลี่ยนช่องบริการ</h2>
        <select v-model="selectedServiceNumber" class="border border-gray-300 p-2 rounded w-full mb-4">
          <option value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
        </select>
        <div class="flex justify-around">
          <button @click="confirmChangeService" class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700">ยืนยัน</button>
          <button @click="cancelChangeService" class="bg-gray-500 text-white px-4 py-2 rounded hover:bg-gray-700">ยกเลิก</button>
        </div>
      </div>
    </div>

    <div v-if="showDeleteCard" class="fixed inset-0 flex items-center justify-center bg-gray-500 bg-opacity-50">
      <div class="bg-white border border-gray-300 rounded-lg shadow-lg p-6 w-80 text-center">
        <h2 class="text-xl font-bold mb-4">แน่ใจที่จะลบไหม?</h2>
        <p>แน่ใจที่จะลบไหม?</p>
        <div class="flex justify-around mt-4">
          <button @click="confirmDeleteStaff" class="bg-red-500 text-white px-4 py-2 rounded hover:bg-red-700">ใช่</button>
          <button @click="cancelDelete" class="bg-gray-500 text-white px-4 py-2 rounded hover:bg-gray-700">ไม่</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>