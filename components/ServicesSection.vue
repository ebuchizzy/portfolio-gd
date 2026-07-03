<template>
    <section id="services" class="py-24 px-4 sm:px-6 md:px-12 lg:px-48">
      <div class="w-full flex justify-center items-center flex-col mb-8 sm:mb-12">
        <h2 class="text-primary text-3xl sm:text-4xl font-bold relative pb-8 text-center" data-aos="fade-up">
          My Services
          <span class="absolute w-24 sm:w-36 h-1 bg-primary bottom-4 left-1/2 transform -translate-x-1/2"></span>
          <span class="absolute w-3 h-3 bg-primary rounded-full bottom-3 left-1/2 transform -translate-x-1/2"></span>
        </h2>
        <p class="text-center w-full md:w-4/5 lg:w-3/5 text-sm sm:text-base" data-aos="fade-up" data-aos-delay="200">
          I specialize in creating visually stunning and highly functional digital experiences. From sleek websites and intuitive user interfaces to compelling brand identities, I bring ideas to life with creativity and technical expertise. Whether you need a modern website or a standout brand design, I’ve got you covered.
        </p>
      </div>
      
      <div class="flex flex-wrap justify-center">
        <div v-for="(service, index) in services" :key="index"
             class="w-full min-[280px]:w-64 sm:w-80 bg-white rounded-lg shadow-lg m-2 sm:m-4 p-4 sm:p-8 flex flex-col items-center transition-all duration-300 hover:bg-primary group"
             :data-aos="service.animation" data-aos-duration="1000" data-aos-delay="400">
          <div class="text-6xl sm:text-8xl text-primary mb-4 sm:mb-6 transition-all duration-300 group-hover:text-white group-hover:-translate-y-2">
            <i :class="service.icon"></i>
          </div>
          <div class="text-center">
            <h3 class="text-lg sm:text-xl font-bold mb-2 sm:mb-3 text-primary transition-all duration-300 group-hover:text-white group-hover:-translate-y-2">
              {{ service.title }}
            </h3>
            <p class="text-sm sm:text-base transition-all duration-300 group-hover:text-white">
              {{ service.description }}
            </p>
          </div>
        </div>
      </div>
    </section>
  </template>
  
  <script setup>
  const services = [
    {
      title: 'Web Design',
      description: 'I craft visually appealing and user-friendly designs using Canva, Figma, Framer, and Spline, ensuring a seamless and engaging user experience.',
      icon: 'fas fa-palette',
      animation: 'fade-right'
    },
    {
      title: 'Graphic Design',
      description: 'With Adobe Creative Suite, I create high-quality designs for branding, marketing, and digital content, helping businesses stand out with compelling visuals.',
      icon: 'fas fa-object-group',
      animation: 'fade-up'
    },
    // {
    //   title: 'Web Development',
    //   description: 'I build dynamic and scalable web applications using HTML, CSS, JavaScript, Vue.js, Nuxt.js, Tailwind CSS for Front-end, Node.js, Express.js, Python, Django for Back-end and mySQL, MongoDB for Database',
    //   icon: 'fas fa-file-code',
    //   animation: 'fade-left'
    // }
  ];
  </script>