<template>
  <section
    id="main"
    class="relative flex h-screen w-full items-center justify-center overflow-hidden bg-[#000716] px-4 sm:px-6 md:px-12 lg:px-48"
  >
    <div class="pointer-events-none absolute inset-0 bg-[radial-gradient(circle_at_top_left,rgba(255,255,255,0.1),transparent_22%),radial-gradient(circle_at_bottom_right,rgba(58,108,244,0.1),transparent_32%),linear-gradient(145deg,#000716_10%,#020c1b_50%,#061020_100%)]"></div>
    <div class="pointer-events-none absolute inset-0 opacity-[0.05] [background-image:linear-gradient(rgba(255,255,255,0.28)_1px,transparent_1px),linear-gradient(90deg,rgba(255,255,255,0.28)_1px,transparent_1px)] [background-size:84px_84px]"></div>

    <div class="relative z-10 text-center max-w-4xl">
      <h2 class="text-white text-2xl sm:text-3xl md:text-3xl lg:text-4xl font-medium" data-aos="fade-right" data-aos-delay="800">
        Hello, I'm <br>
        <span class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-semibold">
          <span>{{ typedText }}</span>
          <span v-if="!typingComplete" class="typing-cursor">|</span>


        </span>
      </h2>
      
      <div class="mt-8 relative h-24 sm:h-28 md:h-36 " data-aos="fade-left" data-aos-delay="900">
        <transition-group name="slide-fade" class="animated-text">
          <h3 :key="currentText"
              class="absolute left-1/2 transform -translate-x-1/2 bg-gradient-to-r from-white via-[#7dd3fc] to-[#3a6cf4] bg-clip-text text-3xl font-bold text-transparent sm:text-4xl md:text-4xl lg:text-6xl">
            {{ currentText }}
          </h3>
        </transition-group>
      </div>
      
      <div class="mt-8 flex flex-col items-center justify-center gap-4 sm:mt-10 sm:flex-row" data-aos="zoom-out" data-aos-delay="1000">
        <NuxtLink
          to="#work"
          class="inline-block rounded-full px-6 py-3 text-base font-semibold uppercase tracking-wider text-white transition-colors duration-500 hover:bg-blue-600 sm:px-8 sm:py-4 sm:text-lg bg-primary"
        >
          See My Works
        </NuxtLink>

        <a
          href="/My%20GDCV.pdf"
          download="My GDCV.pdf"
          class="inline-block rounded-full border border-white/20 bg-white/5 px-6 py-3 text-base font-semibold uppercase tracking-wider text-white transition-colors duration-500 hover:border-primary hover:bg-primary sm:px-8 sm:py-4 sm:text-lg"
        >
          Download CV
        </a>
      </div>
      
      <div class="mt-10 pl-6 sm:mt-14 flex justify-center" data-aos="fade-in" data-aos-delay="1200">
        <a v-for="(icon, index) in socialIcons" :key="index" 
           :href="icon.link" 
           class="text-white text-2xl sm:text-3xl mr-6 sm:mr-8 hover:text-primary transition-colors duration-300"
           :data-aos="'fade-in'"
           :data-aos-delay="1200 + (index * 100)">
          <i :class="icon.class"></i>
        </a>
      </div>
    </div>
  </section>
</template>
  
<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue';

const fullName = "Chukwuebuka Akpuofoba";
const typedText = ref('');
const typingComplete = ref(false);
let typingTimer = null;

const animatedTexts = [
 
  'Web Designer',
  'Graphic Designer',
];

const socialIcons = [
  { class: 'fab fa-behance', link: 'https://www.behance.net/ebukaakpuofoba'},
  { class: 'fab fa-linkedin', link: 'https://www.linkedin.com/in/chukwuebuka-akpuofoba-675b77369'},
  
];

const currentTextIndex = ref(0);
const currentText = computed(() => animatedTexts[currentTextIndex.value]);
let textRotationInterval = null;

const startTypingAnimation = () => {
  let currentIndex = 0;
  typingTimer = setInterval(() => {
    if (currentIndex < fullName.length) {
      typedText.value += fullName.charAt(currentIndex);
      currentIndex++;
    } else {
      clearInterval(typingTimer);
      typingComplete.value = true;
      

      startTextRotation();
    }
  }, 100); 
};

const startTextRotation = () => {
  textRotationInterval = setInterval(() => {
    currentTextIndex.value = (currentTextIndex.value + 1) % animatedTexts.length;
  }, 3000);
};

onMounted(() => {
  
  startTypingAnimation();
});

onUnmounted(() => {

  if (typingTimer) clearInterval(typingTimer);
  if (textRotationInterval) clearInterval(textRotationInterval);
});
</script>
  
<style scoped>
.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  transition: all 0.3s ease;
}
.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateY(20px);
  opacity: 0;
}

.typing-cursor {
  animation: blink 0.7s infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

@media (max-width: 1300px) {
  .three-d {
    scale: 0.7;
    top: 0%;
    right: -20%;
  }
}

@media (max-width: 768px) {
  .three-d {
    scale: 0.5;
    top:-50%;
    right: -20;
  }
}
</style>
