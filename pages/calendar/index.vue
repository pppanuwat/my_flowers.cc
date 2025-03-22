<template>
  <div class="min-h-screen bg-gradient-to-b from-blue-300 to-blue-600 p-4 flex flex-col items-center relative overflow-hidden">
    <div class="absolute top-0 left-0 w-full h-14 bg-pink-500 shadow-lg flex justify-center items-center text-white text-lg font-bold rounded-b-xl">
      📅 Memories Calendar 📅
    </div>

    <div class="w-full max-w-xs mt-20 px-4 flex flex-col items-center">
      <h2 class="text-white text-lg font-bold text-center mb-2">📆 กุมภาพันธ์</h2>
      <div class="grid grid-cols-7 gap-1.5 mb-4">
        <div
          v-for="day in febDays"
          :key="`feb-${day}`"
          class="bg-white p-2 text-sm rounded-lg shadow-md text-center cursor-pointer hover:bg-pink-300 hover:scale-105 transition-all font-semibold"
          @click="viewDay(`feb-${day}`)"
        >
          {{ day }}
        </div>
      </div>
      
      <h2 class="text-white text-lg font-bold text-center mb-2">📆 มีนาคม</h2>
      <div class="grid grid-cols-7 gap-1.5">
        <div
          v-for="day in marDays"
          :key="`mar-${day}`"
          class="bg-white p-2 text-sm rounded-lg shadow-md text-center cursor-pointer hover:bg-pink-300 hover:scale-105 transition-all font-semibold"
          @click="viewDay(`mar-${day}`)"
        >
          {{ day }}
        </div>
      </div>
    </div>

    <button
      @click="goBack"
      class="mt-6 px-6 py-3 bg-pink-500 text-white text-md font-bold rounded-full shadow-lg hover:bg-pink-600 transition-transform transform hover:scale-110 mb-10"
    >
      กลับไปหน้าแรก 💜
    </button>
  </div>
</template>

<script setup lang="ts">
const router = useRouter();

const febDays = Array.from({ length: 29 }, (_, i) => i + 1); // กุมภาพันธ์ 29 วัน
const marDays = Array.from({ length: 31 }, (_, i) => i + 1); // มีนาคม 31 วัน

const viewDay = (day: string) => {
  router.push(`/calendar/${day}`);
};

const goBack = () => {
  router.push("/");
};
</script>
