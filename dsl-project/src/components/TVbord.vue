<template>
  <div class="bg-blue-900 h-[650px] flex flex-col items-center py-16 pr-16">
    <div class="flex space-x-10">
      <!-- กล่องแสดงหมายเลขคิวและจำนวนคนรอ -->
      <div class="flex flex-col space-y-12">
        <!-- คิวหมายเลข -->
        <div class="bg-white rounded-xl shadow-md p-8 text-center w-[320px] h-[300px] flex flex-col justify-between border-2 border-black">
          <p class="text-2xl font-bold text-black ">คิวหมายเลข</p>
          <p class="text-7xl font-bold text-blue-900">44</p>
          <p></p>
          <p></p>
          <p></p>
          <p></p>
          <p></p>
          <p></p>
          <p></p>
          <p></p>
          <p class="text-xl font-bold text-black">ช่องบริการ</p>
          <p class="text-6xl font-bold text-blue-900">1</p>
        </div>
        <!-- จำนวนคนรอ -->
        <div class="bg-white rounded-xl shadow-md p-6 text-center w-[320px] h-[180px] flex flex-col justify-center border-2 border-black">
          <p class="text-3xl font-bold text-black">จำนวนคนรอคิว</p>
          <p class="text-6xl font-bold text-blue-900">8</p>
        </div>
      </div>

      <!-- ตารางช่องบริการ -->
      <div class="bg-white rounded-xl shadow-md w-[900px] border-2 border-black">
        <!-- Header ตาราง -->
        <div class="flex justify-between items-center  text-white p-6 rounded-t-xl">
          <p class="font-bold text-5xl text-black">ช่องบริการ</p>
          <p class="font-bold text-5xl text-black">หมายเลขคิว</p>
        </div>
        <!-- เนื้อหาในตาราง -->
        <div class="divide-y divide-gray-600 ">
          <!-- แถว 1 -->
          <div class="flex justify-between items-center p-6">
            <p class="text-8xl font-bold text-black">1</p>
            <p class="text-8xl font-bold text-blue-900">45</p>
          </div>
          <!-- แถว 2 -->
          <div class="flex justify-between items-center p-6">
            <p class="text-8xl font-bold text-black">2</p>
            <p class="text-8xl font-bold text-blue-900">47</p>
          </div>
          <!-- แถว 3 -->
          <div class="flex justify-between items-center p-6">
            <p class="text-8xl font-bold text-black">3</p>
            <p class="text-8xl font-bold text-blue-900">46</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
</script>
