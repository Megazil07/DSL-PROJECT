<template>
  <div class="queue-display border-2 border-black flex justify-around items-center p-5 relative h-[500px]">
    <div class="service-section text-center">
      <p class="font-bold text-2xl">ช่องบริการที่</p>
      <p class="text-9xl">{{ serviceChannel }}</p>
    </div>
    <div class="queue-section text-center flex flex-col justify-center">
      <div v-if="currentItemInService" class="w-64 border rounded-lg shadow-lg text-center p-6 flex flex-col justify-between h-[400px] relative">
        <div class="flex flex-col items-center">
          <div class="text-4xl font-bold">{{ currentItemInService.queueNumber }}</div>
          <div class="text-sm text-gray-500 mt-2">
            วันที่ {{ currentItemInService.dateTime }}
          </div>
          <div class="custom-topic mt-4">
            {{ currentItemInService.topic }}
          </div>
          <div class="text-xl font-bold mt-4">
            {{ currentItemInService.studentId }}
          </div>
          <div :class="currentItemInService.isBooked ? 'text-green-500' : 'text-red-500'" class="font-bold mt-6 text-xl">
            {{ currentItemInService.isBooked ? 'มีการจองล่วงหน้า' : 'ไม่มีการจองล่วงหน้า' }}
          </div>
        </div>
      </div>
      <div v-if="currentItemInService" class="absolute right-60 flex flex-col space-y-4">
        <button @click="openConfirmModal('skip', currentItemInService)" class="bg-red-500 text-white px-10 py-7 rounded-lg">
          ข้ามคิว
        </button>
        <button @click="recallQueue(currentItemInService)" class="bg-blue-500 text-white px-10 py-7 rounded-lg">
          เรียกซ้ำ
        </button>
        <button @click="completeService" class="bg-green-500 text-white px-10 py-7 rounded-lg">
          เสร็จสิ้น
        </button>
      </div>
    </div>
    <div class="queue-section text-center">
      <p v-if="!currentItemInService" class="text-6xl text-green-500">ว่าง</p>
    </div>
  </div>

  <div class="flex flex-wrap justify-center gap-6 mt-10">
    <div v-for="(item, index) in queueData" :key="index" class="w-64 border rounded-lg shadow-lg text-center p-6 flex flex-col justify-between h-[400px]">
      <div class="flex flex-col items-center">
        <div class="text-4xl font-bold">{{ item.queueNumber }}</div>
        <div class="text-sm text-gray-500 mt-2">
          วันที่ {{ item.dateTime }}
        </div>
        <div class="custom-topic mt-4">
          {{ item.topic }}
        </div>
        <div class="text-xl font-bold mt-4">
          {{ item.studentId }}
        </div>
        <div :class="item.isBooked ? 'text-green-500' : 'text-red-500'" class="font-bold mt-6 text-xl">
          {{ item.isBooked ? 'มีการจองล่วงหน้า' : 'ไม่มีการจองล่วงหน้า' }}
        </div>
      </div>
      <div class="mt-6 flex justify-center space-x-4">
        <button @click="openConfirmModal('skip', item)" class="bg-red-500 text-white px-6 py-2 rounded-lg">
          ข้ามคิว
        </button>
        <button @click="openConfirmModal('call', item)" class="bg-blue-500 text-white px-6 py-2 rounded-lg">
          เรียกคิว
        </button>
      </div>
    </div>
  </div>

  <div v-if="isModalOpen" class="fixed inset-0 bg-gray-500 bg-opacity-50 flex justify-center items-center">
    <div class="bg-white p-6 rounded-lg shadow-lg w-96">
      <p class="text-xl font-bold text-center">
        {{ modalMessage }}
      </p>
      <div class="flex justify-around mt-4">
        <button @click="closeModal" class="bg-red-500 text-white px-6 py-2 rounded-lg">
          ยกเลิก
        </button>
        <button @click="confirmAction" class="bg-green-500 text-white px-6 py-2 rounded-lg">
          ยืนยัน
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'QueueDisplay',
  data() {
    return {
      serviceChannel: 1,
      queueData: [
        { queueNumber: '1', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'แบบคำขอกู้ยืม', studentId: '6531501117', isBooked: true },
        { queueNumber: '2', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'แบบคำขอกู้ยืม', studentId: '6531501117', isBooked: true },
        { queueNumber: '3', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'สัญญากู้ยืม และ แบบเบิกเงินกู้ยืม', studentId: '6531501117', isBooked: false },
        { queueNumber: '4', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'แบบคำขอกู้ยืม', studentId: '6531501117', isBooked: true },
        { queueNumber: '5', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'อื่นๆ', studentId: '6531501117', isBooked: false },
        { queueNumber: '6', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'สัญญากู้ยืม และ แบบเบิกเงินกู้ยืม', studentId: '6531501117', isBooked: true },
        { queueNumber: '7', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'สัญญากู้ยืม และ แบบเบิกเงินกู้ยืม', studentId: '6531501117', isBooked: false },
        { queueNumber: '8', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'แบบคำขอกู้ยืม', studentId: '6531501117', isBooked: true },
        { queueNumber: '9', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'อื่นๆ', studentId: '6531501117', isBooked: false },
        { queueNumber: '10', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'สัญญากู้ยืม และ แบบเบิกเงินกู้ยืม', studentId: '6531501117', isBooked: true },
        { queueNumber: '11', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'สัญญากู้ยืม และ แบบเบิกเงินกู้ยืม', studentId: '6531501117', isBooked: false },
        { queueNumber: '12', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'แบบคำขอกู้ยืม', studentId: '6531501117', isBooked: true },
        { queueNumber: '13', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'อื่นๆ', studentId: '6531501117', isBooked: false },
        { queueNumber: '14', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'สัญญากู้ยืม และ แบบเบิกเงินกู้ยืม', studentId: '6531501117', isBooked: true },
        { queueNumber: '15', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'สัญญากู้ยืม และ แบบเบิกเงินกู้ยืม', studentId: '6531501117', isBooked: false },
        { queueNumber: '16', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'แบบคำขอกู้ยืม', studentId: '6531501117', isBooked: true },
        { queueNumber: '17', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'อื่นๆ', studentId: '6531501117', isBooked: false },
        { queueNumber: '18', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'สัญญากู้ยืม และ แบบเบิกเงินกู้ยืม', studentId: '6531501117', isBooked: true },
        { queueNumber: '19', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'สัญญากู้ยืม และ แบบเบิกเงินกู้ยืม', studentId: '6531501117', isBooked: false },
        { queueNumber: '20', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'แบบคำขอกู้ยืม', studentId: '6531501117', isBooked: true },
        { queueNumber: '21', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'อื่นๆ', studentId: '6531501117', isBooked: false },
        { queueNumber: '22', dateTime: '17 มกราคม 2568 13:00 น.', topic: 'สัญญากู้ยืม และ แบบเบิกเงินกู้ยืม', studentId: '6531501117', isBooked: true }
      ],
      isModalOpen: false,
      modalMessage: '',
      actionType: '',
      currentItem: null,
      currentItemInService: null
    };
  },
  
  methods: {
    openConfirmModal(actionType, item) {
      this.actionType = actionType;
      this.currentItem = item;
      if (actionType === 'call') {
        this.modalMessage = `คุณแน่ใจที่จะ เรียก คิว ${item.queueNumber}`;
      } else if (actionType === 'skip') {
        this.modalMessage = `คุณแน่ใจที่จะ ข้าม คิว ${item.queueNumber}`;
      }
      this.isModalOpen = true;
    },
    closeModal() {
      this.isModalOpen = false;
    },
    confirmAction() {
      if (this.actionType === 'call') {
        this.currentItemInService = this.currentItem;
        this.queueData = this.queueData.filter(item => item.queueNumber !== this.currentItem.queueNumber);
        const message = `เชฺิญหมายเลข ${this.currentItem.queueNumber} ที่ช่องบริการ ${this.serviceChannel}`;
        alert(message);
        this.speakThai(message); // เรียกเสียงอ่านภาษาไทย
      } else if (this.actionType === 'skip') {
        if (this.currentItemInService && this.currentItemInService.queueNumber === this.currentItem.queueNumber) {
          this.currentItemInService = null;
        }
        this.queueData = this.queueData.filter(item => item.queueNumber !== this.currentItem.queueNumber);
        alert(`คิว ${this.currentItem.queueNumber} ถูกข้ามไปแล้ว`);
      }
      this.closeModal();
    },
    recallQueue(item) {
      const message = `เชิญหมายเลข ${item.queueNumber} ที่ช่องบริการ ${this.serviceChannel} `;
      alert(message);
      this.speakThai(message); // เรียกเสียงอ่านภาษาไทย
      this.currentItemInService = item;
    },
    completeService() {
      alert(`บริการคิว ${this.currentItemInService.queueNumber} เสร็จสิ้น`);
      this.currentItemInService = null;
    },
    speakThai(message) {
      if ('speechSynthesis' in window) {
        const utterance = new SpeechSynthesisUtterance(message);
        utterance.lang = 'th-TH'; // ตั้งค่าเป็นภาษาไทย
        utterance.rate = 0.2;
        window.speechSynthesis.speak(utterance);
        
      } else {
        console.warn('Speech Synthesis API ไม่รองรับในเบราว์เซอร์นี้');
      }
    },
    openConfirmModal(actionType, item) {
  // ถ้ามีคิวในช่องบริการอยู่ และกด "เรียกคิว" ให้แสดงข้อความเตือน
  if (actionType === 'call' && this.currentItemInService) {
    alert(`ไม่สามารถเรียกคิวใหม่ได้ เนื่องจากมีคิว ${this.currentItemInService.queueNumber} อยู่ในช่องบริการ กรุณากด "เสร็จสิ้น" ก่อน`);
    return;
  }

  this.actionType = actionType;
  this.currentItem = item;
  if (actionType === 'call') {
    this.modalMessage = `คุณแน่ใจที่จะ เรียก คิว ${item.queueNumber}`;
  } else if (actionType === 'skip') {
    this.modalMessage = `คุณแน่ใจที่จะ ข้าม คิว ${item.queueNumber}`;
  }
  this.isModalOpen = true;
}

  }
};
</script>

<style scoped>
.custom-topic {
  font-size: 20px;
  font-weight: 800;
  color: #1d4ed8;
}
</style>
