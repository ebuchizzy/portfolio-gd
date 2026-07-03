<template>
  <section id="contact" class="py-24 px-4 sm:px-6 md:px-12 lg:px-48 max-w-full overflow-x-hidden">
    <div class="w-full flex justify-center items-center flex-col mb-12 sm:mb-16">
      <h2 class="text-primary text-3xl sm:text-4xl font-bold relative pb-8 text-center" data-aos="fade-up">
        Contact Me
        <span class="absolute w-24 sm:w-36 h-1 bg-primary bottom-4 left-1/2 transform -translate-x-1/2"></span>
        <span class="absolute w-3 h-3 bg-primary rounded-full bottom-3 left-1/2 transform -translate-x-1/2"></span>
      </h2>
    </div>
    
    <div class="flex flex-col space-y-8 sm:space-y-12">
      <div class="flex flex-wrap justify-center">
        <div v-for="(info, index) in contactInfo" :key="index"
             class="w-full min-[280px]:w-64 sm:w-72 bg-white rounded-lg shadow-lg m-2 sm:m-4 p-4 sm:p-6 flex flex-col items-center"
             data-aos="fade-up" :data-aos-delay="100 * (index + 1)">
          <div class="text-4xl sm:text-5xl text-primary mb-3 sm:mb-4 transition-transform duration-500 hover:-translate-y-2">
            <i :class="info.icon"></i>
          </div>
          <div class="text-center w-full">
            <h3 class="text-base sm:text-lg font-bold mb-2">{{ info.title }}</h3>
            <span v-for="(item, i) in info.details" :key="i" class="block text-gray-600 text-xs sm:text-sm break-words">
              <a v-if="info.isLink" :href="item" target="_blank"
                  class="hover:text-primary transition-colors duration-300 truncate block overflow-hidden text-ellipsis max-w-full">
                {{ item.replace('https://www.', '').replace('https://', '') }}
              </a>
              <span v-else>{{ item }}</span>
            </span>
          </div>
        </div>
      </div>
      
      <div class="flex justify-center" data-aos="fade-up" data-aos-delay="400">
        <form
  action="https://formspree.io/f/xojaarkw"
  method="POST"
  class="w-full max-w-2xl bg-white rounded-lg shadow-lg p-4 sm:p-6 md:p-10"
>
  <h3 class="text-xl sm:text-2xl font-semibold text-center mb-6 sm:mb-8">
    Send Message
  </h3>

  <div class="mb-4 sm:mb-6">
    <input
      type="text"
      name="name"
      placeholder="Name"
      required
      class="w-full p-2 sm:p-3 border border-gray-400 rounded-md focus:outline-none focus:ring-2 focus:ring-primary text-sm sm:text-base"
    >
  </div>

  <div class="mb-4 sm:mb-6">
    <input
      type="email"
      name="email"
      placeholder="Email"
      required
      class="w-full p-2 sm:p-3 border border-gray-400 rounded-md focus:outline-none focus:ring-2 focus:ring-primary text-sm sm:text-base"
    >
  </div>

  <div class="mb-4 sm:mb-6">
    <textarea
      name="message"
      rows="6"
      placeholder="Message"
      required
      class="w-full p-2 sm:p-3 border border-gray-400 rounded-md focus:outline-none focus:ring-2 focus:ring-primary text-sm sm:text-base"
    ></textarea>
  </div>

  <button
    type="submit"
    class="w-full py-2 sm:py-3 bg-primary text-white font-medium uppercase tracking-wider rounded-md transition-colors duration-300 hover:bg-blue-600 text-sm sm:text-base"
  >
    Send
  </button>
</form>

      </div>
    </div>
  </section>
</template>

<script setup>
const contactInfo = [
  {
    title: 'Address',
    details: ['Lagos, Nigeria'],
    icon: 'fas fa-map-marker-alt',
    isLink: false
  },
  {
    title: 'Phone',
    details: ['+2347065038527'],
    icon: 'fas fa-phone',
    isLink: false
  },
  {
    title: 'Email Address',
    details: ['emmanuelakpuofoba@gmail.com'],
    icon: 'fas fa-envelope',
    isLink: false
  },
  {
    title: 'Portfolio',
    details: [
      'https://www.behance.net/ebukaakpuofoba',
      'https://www.linkedin.com/in/chukwuebuka-akpuofoba-675b77369',
      'https://github.com/ebuchizzy?tab=repositories'
    ],
    icon: 'fas fa-globe',
    isLink: true
  }
];
</script>

<style scoped>
body, html {
  overflow-x: hidden;
  width: 100%;
  max-width: 100%;
  position: relative;
}

.break-words {
  word-break: break-word;
}

a.truncate {
  max-width: 100%;
}
</style>