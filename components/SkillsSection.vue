<template>
  <section
    id="skills"
    class="relative isolate overflow-hidden bg-[#000716] px-4 py-24 text-white sm:px-6 sm:py-24 md:px-12 lg:px-48"
  >
    <div class="pointer-events-none absolute inset-0 bg-[radial-gradient(circle_at_top_left,rgba(255,255,255,0.08),transparent_22%),radial-gradient(circle_at_top_right,rgba(125,211,252,0.08),transparent_24%),linear-gradient(135deg,#000512_14%,#020a18_48%,#050d1a_100%)]"></div>
    <div class="pointer-events-none absolute inset-0 opacity-[0.04] [background-image:linear-gradient(rgba(255,255,255,0.26)_1px,transparent_1px),linear-gradient(90deg,rgba(255,255,255,0.26)_1px,transparent_1px)] [background-size:72px_72px]"></div>

    <div class="relative z-10 mb-8 flex w-full flex-col items-center justify-center sm:mb-16">
      <h2 class="relative pb-8 text-center text-2xl font-bold text-primary sm:text-4xl" data-aos="fade-up">
        My Skills
        <span class="absolute bottom-4 left-1/2 h-1 w-24 -translate-x-1/2 transform bg-primary sm:w-36"></span>
        <span class="absolute bottom-3 left-1/2 h-3 w-3 -translate-x-1/2 transform rounded-full bg-primary"></span>
      </h2>
    </div>

    <div class="relative z-10 grid gap-10 lg:grid-cols-[minmax(0,0.95fr)_minmax(0,1.05fr)] lg:items-start">
      <div>
        <h2
          class="mb-4 text-center text-xl font-bold sm:mb-6 sm:text-3xl lg:text-left"
          data-aos="fade-right"
          data-aos-delay="200"
        >
          My Skills and Experiences
        </h2>
        <p class="mb-6 text-sm leading-7 text-white/75 sm:mb-8 sm:text-base" data-aos="flip-down" data-aos-delay="300">
       My graphic design expertise, allows me to develop compelling visuals that strengthen brand identity and communication. Whether it's design or branding, I ensure every project is both aesthetically striking and strategically effective.  I specialize in crafting visually appealing and highly functional digital experiences. As a Graphic designer and Web designer, I use Adobe Creative Cloud Suite, Canva, Figma, Framer, and Spline to create sleek, user-friendly interfaces that enhance engagement and usability. 
        </p>

        <!-- <p class="mb-6 text-sm leading-7 text-white/75 sm:mb-8 sm:text-base" data-aos="flip-down" data-aos-delay="350">
          On the development side, I build dynamic and scalable web applications using HTML, CSS, JavaScript, Python, REST APIs and Git, leveraging frameworks like Vue.js, Nuxt.js, and Tailwind CSS for modern front-end solutions. My backend expertise includes Node.js, Express.js, Django, MongoDB, and mySQL, enabling me to create seamless, high-performance applications. From concept to deployment, I provide full-stack solutions that merge creativity with functionality to bring ideas to life.
        </p> -->
      </div>

      <div class="grid gap-5 sm:grid-cols-2">
        <article
          v-for="(skill, index) in skills"
          :key="skill.name"
          class="group relative z-0 overflow-hidden rounded-[28px] border border-white/10 bg-[#081425] p-6 shadow-[0_20px_60px_rgba(0,0,0,0.28)] transition-all duration-300 ease-out transform-gpu hover:z-20 hover:-translate-y-3 hover:scale-[1.1] hover:border-primary/40 hover:shadow-[0_28px_80px_rgba(58,108,244,0.28)]"
          data-aos="fade-up"
          :data-aos-delay="120 + (index * 80)"
        >
          <div class="pointer-events-none absolute inset-0 bg-[radial-gradient(circle_at_top_left,rgba(58,108,244,0.18),transparent_42%)] opacity-80"></div>
          <div class="relative z-10">
            <div class="mb-8 flex items-start justify-between gap-4">
              <div
                class="flex h-12 w-12 items-center justify-center rounded-2xl border border-white/10 bg-white/[0.03] text-lg font-semibold text-white/90 transition-transform duration-300 ease-out group-hover:scale-110"
                :class="skill.iconColor"
              >
                {{ skill.icon }}
              </div>

              <span class="rounded-full border border-white/10 px-3 py-1 text-[11px] font-semibold uppercase tracking-[0.22em] text-white/45">
                {{ skill.category }}
              </span>
            </div>

            <h3 class="mb-3 text-2xl font-semibold tracking-tight text-white">{{ skill.name }}</h3>
            <p class="text-sm leading-7 text-white/65 sm:text-[15px]">
              {{ skill.description }}
            </p>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
const skills = [
  // {
  //   name: 'Nuxt.js',
  //   category: 'Frontend',
  //   icon: 'N',
  //   iconColor: 'text-[#7CFFB2]',
  //   description: 'Vue-powered framework for building fast, SEO-friendly websites and smooth application experiences.'
  // },
  // {
  //   name: 'Vue.js',
  //   category: 'Frontend',
  //   icon: 'V',
  //   iconColor: 'text-[#5EE9AE]',
  //   description: 'Component-driven UI development for clean, maintainable interfaces and responsive product flows.'
  // },
  // {
  //   name: 'JavaScript',
  //   category: 'Core',
  //   icon: 'JS',
  //   iconColor: 'text-[#FFD84D]',
  //   description: 'Interactive behavior, reusable logic, and modern browser features for dynamic web applications.'
  // },
  // {
  //   name: 'Tailwind CSS',
  //   category: 'UI Styling',
  //   icon: 'TW',
  //   iconColor: 'text-[#7DE7FF]',
  //   description: 'Utility-first styling system that helps me build refined layouts quickly without losing design control.'
  // },
  // {
  //   name: 'TypeScript',
  //   category: 'Frontend',
  //   icon: 'TS',
  //   iconColor: 'text-[#67A6FF]',
  //   description: 'Strong typing for safer refactors, clearer architecture, and more predictable large-scale codebases.'
  // },
  {
    name: 'Figma',
    category: 'Design',
    icon: 'FG',
    iconColor: 'text-[#FF8B9B]',
    description: 'Interface design and collaborative product planning for wireframes, polished UI systems, and design handoff.'
  },
  {
    name: 'Spline',
    category: 'Design',
    icon: 'SP', // Or a custom 3D icon if you prefer
    iconColor: 'text-[#FF8B9B]', // Spline's signature vibrant orange
    description: '3D design and interactive web asset creation for immersive interfaces, real-time animations, and web embeds.'
  },
  {
    name: 'Canva',
    category: 'Design',
    icon: 'CV',
    iconColor: 'text-[#FF8B9B]', // Canva's distinct cyan/teal color
    description: 'Rapid asset creation and template ecosystem deployment for quick marketing collateral, social media posts, and client accessible documents.'
  },
  {
    name: 'Framer',
    category: 'Design',
    icon: 'FR',
    iconColor: 'text-[#A7B7FF]',
    description: 'Interactive prototyping and modern site design workflows for smooth presentation, motion, and layout exploration.'
  },
  {
    name: 'Adobe Creative Cloud',
    category: 'Design',
    icon: 'CC',
    iconColor: 'text-[#FF6B6B]',
    description: 'Creative toolkit I use for brand visuals, image editing, marketing assets, and polished graphic design work.'
  },
  // {
  //   name: 'Node.js',
  //   category: 'Backend',
  //   icon: 'ND',
  //   iconColor: 'text-[#8CE46D]',
  //   description: 'Server-side runtime for APIs, app logic, and scalable services that support full-stack delivery.'
  // },
  // {
  //   name: 'Express.js',
  //   category: 'Backend',
  //   icon: 'EX',
  //   iconColor: 'text-[#C2D1FF]',
  //   description: 'Minimal backend framework I use for routing, REST APIs, middleware, and lightweight server architecture.'
  // },
  // {
  //   name: 'Python',
  //   category: 'Backend',
  //   icon: 'PY',
  //   iconColor: 'text-[#FFD15C]',
  //   description: 'Versatile programming language for backend systems, automation, data-driven logic, and scalable application features.'
  // },
  // {
  //   name: 'Django',
  //   category: 'Backend',
  //   icon: 'DJ',
  //   iconColor: 'text-[#78F0C8]',
  //   description: 'Robust Python framework for building secure, structured web applications with strong admin and database tooling.'
  // },
  // {
  //   name: 'MySQL',
  //   category: 'Database',
  //   icon: 'MY',
  //   iconColor: 'text-[#7DD3FC]',
  //   description: 'Relational database management for structured application data, queries, and dependable backend persistence.'
  // },
  // {
  //   name: 'MongoDB',
  //   category: 'Database',
  //   icon: 'MG',
  //   iconColor: 'text-[#86EFAC]',
  //   description: 'Document-based database solution for flexible schemas, rapid iteration, and scalable full-stack applications.'
  // }
];
</script>
