<template>
  <div
    class="min-h-screen flex flex-col items-center justify-center bg-purple-100 p-6"
  >
    <motion-div
      @click="goToGallery"
      class="relative bg-purple-300 p-10 rounded-2xl shadow-lg text-center cursor-pointer hover:bg-purple-200"
      :initial="{ scale: 0 }"
      :animate="{ scale: 1 }"
      :transition="{ duration: 0.5 }"
    >
      <Sparkles
        class="absolute top-[-10px] right-[-10px] text-yellow-300 animate-ping"
        size="24"
      />
      <h1 class="text-3xl font-bold text-purple-700">CreamCream</h1>
      <p class="mt-4 text-lg text-purple-600">{{ message }}</p>
    </motion-div>

  </div>
</template>

<script setup lang="ts">
const message = ref("");
const router = useRouter();

onMounted(() => {
  const text = "💜 💜 💜";
  let index = 0;
  const interval = setInterval(() => {
    message.value += text[index];
    index++;
    if (index === text.length) clearInterval(interval);
  }, 200);
});

const goToGallery = () => {
  router.push("/gallery");
};
</script>

<style scoped></style>
