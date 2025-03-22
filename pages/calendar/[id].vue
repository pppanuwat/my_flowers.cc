<template>
  <div
    class="min-h-screen bg-gradient-to-b from-purple-200 to-purple-500 p-4 flex flex-col items-center relative overflow-hidden"
  >
    <div
      class="absolute top-0 left-0 w-full h-14 bg-pink-500 shadow-lg flex justify-center items-center text-white text-lg font-bold rounded-b-xl"
    >
      📸 Memories of {{ dayLabel }} 📸
    </div>

    <div class="w-full max-w-md mt-20 px-4 flex flex-col items-center">
      <div class="grid grid-cols-3 gap-2 w-full">
        <div
          v-for="(image, index) in images"
          :key="index"
          class="relative group overflow-hidden rounded-lg shadow-lg border-4 border-white transition-transform transform hover:scale-105"
        >
          <img
            :src="image"
            class="w-full h-auto object-cover group-hover:opacity-90 rounded-lg"
          />
        </div>
      </div>
    </div>

    <button
      @click="goBack"
      class="mt-6 px-6 py-3 bg-pink-500 text-white text-md font-bold rounded-full shadow-lg hover:bg-pink-600 transition-transform transform hover:scale-110 mb-10"
    >
      🔙 กลับไปปฏิทิน
    </button>
  </div>
</template>

<script setup lang="ts">

const router = useRouter();
const route = useRoute();
const dayLabel = computed(() => route.params.day);

const images = ref([
  "https://source.unsplash.com/random/200x200?sig=1",
  "https://source.unsplash.com/random/200x200?sig=2",
  "https://source.unsplash.com/random/200x200?sig=3",
  "https://source.unsplash.com/random/200x200?sig=4",
  "https://source.unsplash.com/random/200x200?sig=5",
  "https://source.unsplash.com/random/200x200?sig=6",
]);

const goBack = () => {
  router.push("/calendar");
};
</script>
