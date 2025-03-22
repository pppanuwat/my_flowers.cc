<template>
  <div
    class="min-h-screen bg-gradient-to-b from-blue-300 to-blue-600 p-4 flex flex-col items-center relative overflow-hidden"
  >
    <div
      class="absolute top-0 left-0 w-full h-14 bg-pink-500 shadow-lg flex justify-center items-center text-white text-lg font-bold rounded-b-xl"
    >
      📅 Memories Calendar 📅
    </div>

    <div class="w-full max-w-md mt-20 px-4 flex flex-col items-center">
      <h2 class="text-white text-lg font-bold text-center mb-2">
        📆 กุมภาพันธ์
      </h2>
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

    <div
      v-if="selectedDay && images[selectedDay]"
      class="mt-6 p-4 bg-white rounded-lg shadow-lg max-w-xs w-full"
    >
      <h3 class="text-lg font-bold text-center mb-2">
        📸 รูปภาพของ {{ selectedDay }}
      </h3>
      <div
        class="grid grid-cols-2 gap-2 overflow-x-auto max-h-60 p-2 scrollbar-hide"
      >
        <img
          v-for="img in images[selectedDay]"
          :key="img"
          :src="img"
          class="w-full rounded-lg shadow-md border-2 border-pink-300"
        />
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

const febDays = Array.from({ length: 29 }, (_, i) => i + 1);
const marDays = Array.from({ length: 31 }, (_, i) => i + 1);

const selectedDay = ref<string | null>(null);
const images = ref<{ [key: string]: string[] }>({
  "feb-1": ["/images/feb1-1.jpg", "/images/feb1-2.jpg"],
  "mar-5": ["/images/mar5-1.jpg", "/images/mar5-2.jpg"],
});

const viewDay = (day: string) => {
  selectedDay.value = day;
};

const goBack = () => {
  router.push("/");
};
</script>

<style>
.scrollbar-hide::-webkit-scrollbar {
  display: none;
}
.scrollbar-hide {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
</style>
