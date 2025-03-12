<template>
  <div
    class="min-h-screen bg-gradient-to-b from-purple-200 to-purple-400 p-6 flex flex-col items-center relative overflow-hidden"
  >
    <div
      class="absolute top-0 left-0 w-full h-20 bg-pink-500 shadow-lg flex justify-center items-center text-white text-xl font-bold rounded-b-xl"
    >
      📸 Cute Memories Booth 📸
    </div>

    <div class="grid grid-cols-2 gap-6 sm:grid-cols-3 md:grid-cols-4 mt-16">
      <div
        v-for="(image, index) in images"
        :key="index"
        class="relative group overflow-hidden rounded-xl shadow-xl border-4 border-white"
      >
        <img
          :src="image"
          class="w-full h-auto object-cover transform transition duration-300 group-hover:scale-110"
        />
        <div
          class="absolute bottom-2 left-2 bg-white px-3 py-1 text-sm font-bold text-pink-500 rounded-md shadow"
        >
          💖 Cute
        </div>
      </div>
    </div>

    <!-- ปุ่มเปิดกล้อง -->
    <button
      @click="openCamera"
      class="mt-4 px-6 py-3 bg-purple-500 text-white font-bold rounded-full shadow-lg hover:bg-purple-600 transition-transform transform hover:scale-105"
    >
      อยากรู้ไหมใครน่ารักที่สุด
    </button>

    <div v-if="showCamera" class="mt-6 relative">
      <video
        ref="video"
        autoplay
        class="w-80 h-60 border-4 border-white rounded-xl shadow-lg transform scale-x-[-1]"
      ></video>
      <button
        @click="takePhoto"
        class="mt-4 px-6 py-3 bg-green-500 text-white font-bold rounded-full shadow-lg hover:bg-green-600"
      >
        ถ่ายรูป 📸
      </button>
    </div>

    <button
      @click="goBack"
      class="mt-6 px-8 py-4 bg-pink-500 text-white text-lg font-bold rounded-full shadow-lg hover:bg-pink-600 transition-transform transform hover:scale-105 mb-24"
    >
      กลับไปหน้าแรก 💜
    </button>
    <div
      class="absolute bottom-0 left-0 w-full h-16 bg-pink-500 shadow-lg flex justify-center items-center text-white text-lg font-semibold rounded-t-xl mt-24"
    >
      🎀 Best Moments Together 🎀
    </div>
  </div>
</template>

<script setup lang="ts">
const router = useRouter();
const images = ref<any>([
  "https://cdn.pixabay.com/photo/2023/09/13/07/29/ghost-8250317_640.png",
  "https://i.pinimg.com/736x/ee/13/e3/ee13e3e1e7de654b62f4d2e364d025cb.jpg",
  "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR8Xq_-VarEZwOMCkqGQyr_L4xCMu_YPe79ZPV0swoxiFsAjFR4rw2znptP4QWOWE4tGAk&usqp=CAU",
  "https://png.pngtree.com/png-clipart/20220228/ourmid/pngtree-cartoon-cute-little-girl-wearing-skirt-hand-painted-illustration-can-be-png-image_4417703.png",
  "https://png.pngtree.com/png-clipart/20220110/ourmid/pngtree-people-and-food-girl-and-food-set-png-image_4287778.png",
]);

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
      ctx.translate(canvas.width, 0); // ย้ายจุดเริ่มต้นของ canvas ไปขวาสุด
      ctx.scale(-1, 1); // พลิกภาพในแนวนอน
      ctx.drawImage(video.value, 0, 0, canvas.width, canvas.height);

      images.value.push(canvas.toDataURL("image/png"));
    }
  }
};

const goBack = () => {
  router.push("/");
};
</script>

<style scoped></style>
