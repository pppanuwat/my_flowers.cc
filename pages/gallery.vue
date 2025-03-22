<template>
  <div
    class="min-h-screen bg-gradient-to-b from-purple-200 to-purple-500 p-4 flex flex-col items-center relative overflow-hidden"
  >
    <div
      class="absolute top-0 left-0 w-full h-16 bg-pink-500 shadow-lg flex justify-center items-center text-white text-lg font-bold rounded-b-xl animate-bounceIn"
    >
      📸 Cute Memories Booth 📸
    </div>

    <div class="grid grid-cols-2 gap-4 sm:grid-cols-3 mt-20 w-full px-4">
      <div
        @click="rounterTo"
        v-for="(image, index) in images"
        :key="index"
        class="relative group overflow-hidden rounded-lg shadow-lg border-4 border-white transition-all transform hover:scale-105 hover:rotate-1 hover:shadow-2xl"
      >
        <img
          :src="image"
          class="w-full h-auto object-cover group-hover:opacity-90 transition-opacity duration-300"
        />
        <div
          class="absolute bottom-2 left-2 bg-white px-3 py-1 text-sm font-bold text-pink-500 rounded-md shadow-md animate-pulse"
        >
          💖 Cute
        </div>
      </div>
    </div>

    <p class="mt-6 text-lg font-semibold text-white text-center drop-shadow-lg">
      อยากรู้ไหมว่าใครน่ารักที่สุด?
    </p>

    <button
      @click="openCamera"
      class="mt-4 px-6 py-3 bg-purple-600 text-white font-bold rounded-full shadow-lg hover:bg-purple-700 transition-all transform hover:scale-110 active:scale-95 animate-wiggle"
    >
      กดๆๆๆๆ
    </button>

    <div v-if="showCamera" class="mt-6 w-full flex flex-col items-center">
      <div class="relative w-full max-w-xs">
        <video
          ref="video"
          autoplay
          class="w-full border-4 border-white rounded-lg shadow-lg transform scale-x-[-1]"
        ></video>
        <button
          @click="takePhoto"
          class="absolute bottom-2 right-2 px-4 py-2 bg-green-500 text-white font-bold rounded-full shadow-lg hover:bg-green-600 transition-transform hover:scale-105"
        >
          📸 ถ่ายรูป
        </button>
      </div>
    </div>

    <button
      @click="toggleMusic"
      class="fixed bottom-4 right-4 px-6 py-3 bg-yellow-500 text-white font-bold rounded-full shadow-lg hover:bg-yellow-600 transition-transform transform hover:scale-110 active:scale-95"
    >
      🎵 {{ isPlaying ? "ปิดเพลง" : "เปิดเพลง" }}
    </button>

    <iframe
      v-show="isPlaying"
      width="0"
      height="0"
      src="https://www.youtube.com/embed/rWCULtx785s?autoplay=1&loop=1&playlist=rWCULtx785s"
      frameborder="0"
      allow="autoplay"
    ></iframe>
  </div>
</template>

<script setup lang="ts">
const router = useRouter();
const images = ref<any>([
  "https://cdn.pixabay.com/photo/2023/09/13/07/29/ghost-8250317_640.png",
  "https://i.pinimg.com/736x/ee/13/e3/ee13e3e1e7de654b62f4d2e364d025cb.jpg",
  "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR8Xq_-VarEZwOMCkqGQyr_L4xCMu_YPe79ZPV0swoxiFsAjFR4rw2znptP4QWOWE4tGAk&usqp=CAU",
]);
const isPlaying = ref(true);
const showCamera = ref(false);
const video = ref<HTMLVideoElement | null>(null);

const openCamera = async () => {
  showCamera.value = true;
  const stream = await navigator.mediaDevices.getUserMedia({ video: true });
  if (video.value) video.value.srcObject = stream;
};

const takePhoto = () => {
  const canvas = document.createElement("canvas");
  if (video.value) {
    canvas.width = video.value.videoWidth;
    canvas.height = video.value.videoHeight;
    const ctx = canvas.getContext("2d");

    if (ctx) {
      ctx.translate(canvas.width, 0);
      ctx.scale(-1, 1);
      ctx.drawImage(video.value, 0, 0, canvas.width, canvas.height);
      images.value.push(canvas.toDataURL("image/png"));
    }
  }
  closeCamera();
};

const closeCamera = () => {
  if (video.value && video.value.srcObject) {
    const stream = video.value.srcObject as MediaStream;
    stream.getTracks().forEach((track) => track.stop());
  }
  showCamera.value = false;
};

const toggleMusic = () => {
  isPlaying.value = !isPlaying.value;
};

const rounterTo = () => {
  router.push("/dump");
};
const goBack = () => {
  router.push("/");
};
</script>

<style scoped>
@keyframes bounceIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes wiggle {
  0%,
  100% {
    transform: rotate(-3deg);
  }
  50% {
    transform: rotate(3deg);
  }
}

.animate-bounceIn {
  animation: bounceIn 0.8s ease-out;
}

.animate-wiggle {
  animation: wiggle 0.5s infinite alternate ease-in-out;
}
</style>
