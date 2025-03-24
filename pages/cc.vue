<template>
  <div class="flex flex-col items-center justify-center h-screen bg-blue-100">
    <div class="bg-white p-6 rounded-2xl shadow-lg text-center">
      <h1 class="text-2xl font-semibold mb-4">เป็นแฟนกันมั้ยครับ? 🥺</h1>
      <div class="flex gap-4">
        <button
          class="px-6 py-2 bg-green-500 text-white font-bold rounded-lg hover:bg-green-600"
          @click="accept"
        >
          เป็น 💖
        </button>
        <button
          ref="noButton"
          class="px-6 py-2 bg-red-500 text-white font-bold rounded-lg"
          :style="noButtonStyle"
          @mouseover="moveNoButton"
        >
          ไม่เป็น 💔
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">

const noButton = ref<HTMLButtonElement | null>(null);
const noButtonStyle = ref({ position: "relative", left: "0px", top: "0px" });

const moveNoButton = () => {
  const randomX = Math.random() * 200 - 100;
  const randomY = Math.random() * 200 - 100;
  noButtonStyle.value = {
    position: "relative",
    left: `${randomX}px`,
    top: `${randomY}px`,
  };
};

const accept = () => {
  alert("เย้! เราเป็นแฟนกันแล้ว 💖");
};
</script>

<style scoped>
button {
  transition: all 0.3s ease;
}
</style>
