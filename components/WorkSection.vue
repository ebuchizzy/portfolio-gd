<template>
  <section
    id="work"
    class="relative isolate overflow-hidden bg-[#000716] px-4 py-24 sm:px-6 md:px-12 lg:px-20"
  >
    <div class="pointer-events-none absolute inset-0 bg-[radial-gradient(circle_at_top_left,rgba(255,255,255,0.08),transparent_22%),radial-gradient(circle_at_bottom_right,rgba(58,108,244,0.1),transparent_30%),linear-gradient(145deg,#000512_10%,#020a18_52%,#050d1a_100%)]"></div>
    <div class="pointer-events-none absolute inset-0 opacity-[0.04] [background-image:linear-gradient(rgba(255,255,255,0.26)_1px,transparent_1px),linear-gradient(90deg,rgba(255,255,255,0.26)_1px,transparent_1px)] [background-size:80px_80px]"></div>

    <div class="relative z-10 mb-10 flex w-full flex-col items-center justify-center sm:mb-16">
      <h2 class="text-primary relative pb-8 text-center text-2xl font-bold sm:text-4xl" data-aos="fade-up">
        My Works
        <span class="bg-primary absolute bottom-4 left-1/2 h-1 w-24 -translate-x-1/2 transform sm:w-36"></span>
        <span class="bg-primary absolute bottom-3 left-1/2 h-3 w-3 -translate-x-1/2 transform rounded-full"></span>
      </h2>
    </div>

    <div class="relative z-10 grid grid-cols-1 gap-4 sm:gap-5 md:grid-cols-2 xl:grid-cols-3">
      <article
        v-for="(work, index) in works"
        :key="work.title"
        class="group mx-auto w-full max-w-sm overflow-hidden rounded-2xl border border-[#1b2d4f] bg-[#030d24]/55 transition-all duration-300 hover:-translate-y-1 hover:border-primary/50"
        :data-aos="'fade-up'"
        :data-aos-delay="120 + (index % 3) * 120"
      >
        <div class="relative h-44 overflow-hidden border-b border-[#1b2d4f]">
          <img
            :src="work.image"
            :alt="work.title"
            class="h-full w-full object-cover transition-transform duration-500 group-hover:scale-[1.03]"
          >
        </div>

        <div class="space-y-3.5 p-[18px]">
          <div class="flex items-start justify-between gap-3">
            <div>
              <h3 class="text-2xl font-semibold text-white">{{ work.title }}</h3>
              <p class="text-[11px] uppercase tracking-[0.16em] text-slate-400">{{ work.category }}</p>
            </div>
            <button
              type="button"
              class="rounded-full border border-[#2a4068] px-3 py-1 text-[10px] font-semibold uppercase tracking-[0.14em] text-slate-200 transition-colors duration-200 hover:border-primary hover:bg-primary hover:text-[#011122]"
              @click="openWork(work)"
            >
              Details
            </button>
          </div>

          <p class="text-sm leading-relaxed text-slate-300">
            {{ work.excerpt }}
          </p>

          <div class="flex flex-wrap gap-2">
            <span
              v-for="tag in work.tags"
              :key="tag"
              class="rounded-full border border-[#243b62] px-2.5 py-1 text-[10px] font-medium uppercase tracking-[0.12em] text-slate-300"
            >
              {{ tag }}
            </span>
          </div>
        </div>
      </article>
    </div>

    <Teleport to="body">
      <div
        v-if="activeWork"
        class="fixed inset-0 z-[9999] flex items-start justify-center overflow-y-auto bg-black/75 p-3 pt-24 sm:p-6 sm:pt-28"
        @click.self="closeModal"
      >
        <div class="mb-8 w-full max-w-4xl rounded-2xl border border-[#29406b] bg-[#03122f] p-4 shadow-2xl shadow-black/50 sm:p-6">
          <div class="mb-4 flex items-start justify-between gap-4">
            <div>
              <h3 class="text-3xl font-semibold text-white sm:text-4xl">{{ activeWork.title }}</h3>
              <p class="text-[11px] uppercase tracking-[0.16em] text-slate-400">{{ activeWork.category }}</p>
            </div>
            <button
              type="button"
              class="flex h-10 w-10 items-center justify-center rounded-full border border-[#2d4774] bg-[#071a3d] text-2xl leading-none text-slate-200 shadow-lg shadow-black/40 transition-colors hover:border-primary hover:text-primary"
              @click="closeModal"
            >
              ×
            </button>
          </div>

          <div class="mb-6 overflow-hidden rounded-2xl border border-[#1f3057]">
            <img :src="activeWork.image" :alt="activeWork.title" class="h-full w-full object-cover">
          </div>

          <p class="mb-6 text-base leading-relaxed text-slate-300 sm:text-lg">
            {{ activeWork.description }}
          </p>

          <div class="grid grid-cols-1 gap-6 md:grid-cols-2">
            <div>
              <h4 class="mb-3 text-2xl font-semibold text-white">Tech Stack</h4>
              <ul class="space-y-2 text-slate-200">
                <li v-for="tech in activeWork.techStack" :key="tech" class="flex items-center gap-2">
                  <span class="h-2 w-2 rounded-full bg-primary"></span>
                  <span class="text-base">{{ tech }}</span>
                </li>
              </ul>
            </div>

            <div>
              <h4 class="mb-3 text-2xl font-semibold text-white">Key Features</h4>
              <ul class="space-y-2 text-slate-200">
                <li v-for="feature in activeWork.features" :key="feature" class="flex items-center gap-2">
                  <span class="h-2 w-2 rounded-full bg-primary"></span>
                  <span class="text-base">{{ feature }}</span>
                </li>
              </ul>
            </div>
          </div>

          <div class="mt-8">
            <a
              :href="activeWork.link"
              target="_blank"
              rel="noopener noreferrer"
              class="inline-flex items-center rounded-full bg-primary px-8 py-3 text-base font-semibold text-white transition-opacity hover:opacity-85"
            >
              Visit Project
            </a>
          </div>
        </div>
      </div>
    </Teleport>
  </section>
</template>

<script setup>
import { onMounted, onUnmounted, ref, watch } from 'vue';


import image3 from '@/assets/Image/Desktop - 11.png';
import image4 from '@/assets/Image/Frame 4.png';
import image5 from '@/assets/Image/img.png';
import image6 from '@/assets/Image/Desktop - 111.png';
import image8 from '@/assets/Image/MacBook Air - 1.png';
import image9 from '@/assets/Image/Flux.png';
import image10 from '@/assets/Image/Nex.png';
import image11 from '@/assets/Image/Vert.png';
import image12 from '@/assets/Image/Cryenix.png';
import image1 from '@/assets/Image/Desktop - 1.png';
import image2 from '@/assets/Image/Desktop - 2.png';
import image7 from '@/assets/Image/Desk - saint.png';

const works = [
  
  {
    title: 'JSPARKS Logo',
    category: 'Brand Identity',
    excerpt: 'A vibrant branding project balancing visual storytelling and consistency.',
    description:
      'JSPARKS branding focuses on memorable identity assets, modern presentation styles, and cohesive graphic systems tailored for online and print use.',
    tags: ['Branding', 'Identity', 'Creative'],
    techStack: ['Figma', 'Adobe Illustrator',],
    features: ['Logo exploration', 'Color system', 'Typography direction', 'Brand presentation deck'],
    image: image1,
    link: 'https://www.behance.net/gallery/220607569/JSPARKS-branding',
  },
  {
    title: 'JSPARKS Media',
    category: 'Campaign Showcase',
    excerpt: 'Companion showcase with campaign-ready brand applications across mediums.',
    description:
      'This extension of the JSPARKS project highlights campaign mockups and marketing-ready assets to demonstrate practical brand usage in digital channels.',
    tags: ['Campaign', 'Creative', 'Showcase'],
    techStack: ['Figma', 'Photoshop'],
    features: ['Campaign mockups', 'Asset consistency', 'Social-ready layouts', 'Presentation storytelling'],
    image: image2,
    link: 'https://www.behance.net/gallery/220607569/JSPARKS-branding',
  },
  {
    title: 'Lanraj',
    category: 'Brand Identity',
    excerpt: 'Structured product-thinking case study with emphasis on clarity and flow.',
    description:
      'Lanraj combines product strategy and UI execution into a concise case study with intentional user flow design, polished interface language, and actionable outcomes.',
    tags: ['Product', 'UX', 'Case Study'],
    techStack: ['Figma', 'Adobe Illustrator','Adobe Photoshop'],
    features: ['Wireframing', 'UX Research', 'Prototyping','Visual Branding'],
    image: image3,
    link: 'https://www.behance.net/gallery/217027223/Lanraj-Product-Design',
  },
  {
    title: 'Petrofa',
    category: 'Energy Sector Campaign',
    excerpt: 'A polished campaign identity crafted for industrial and digital channels.',
    description:
      'Petrofa showcases strategic visual communication for the energy sector through impactful compositions, clear hierarchy, and reusable campaign assets.',
    tags: ['Campaign', 'Creative', 'Design'],
    techStack: ['Adobe Creative Suite', 'Figma',],
    features: ['Campaign consistency', 'Sector-appropriate visuals', 'Visual Branding'],
    image: image4,
    link: 'https://www.behance.net/gallery/236087981/Petrofa',
  },
  
    
  {
    title: 'Jumaphad',
    category: 'Visual Concept',
    excerpt: 'A concept presentation blending modern aesthetics with practical usage.',
    description:
      'Jumaphad combines visual experimentation with practical screen compositions, resulting in a clean and elegant concept presentation suitable for pitch contexts.',
    tags: ['Campaign', 'Visual', 'Presentation'],
    techStack: ['Figma', 'Photoshop'],
    features: ['High-fidelity mockups', 'Consistent visual language', 'Pitch-ready arrangement', 'Strong composition'],
    image: image8,
    link: 'https://www.behance.net/gallery/228935409/Jumaphad-2',
  },
  {
    title: 'FluxenX',
    category: 'Landing Page Design',
    excerpt: 'A modern product landing page with strong gradients and clear messaging.',
    description:
      'FluxenX explores modern hero composition, component consistency, and clear conversion paths, delivering a memorable product-focused landing page design.',
    tags: ['Landing', 'UI', 'Modern'],
    techStack: ['Figma', 'Spline'],
    features: ['Hero-first storytelling', 'Scalable component blocks', 'Clear conversion prompts', 'Interaction Prototyping'],
    image: image9,
    link: 'https://www.behance.net/gallery/235036049/FluxenX-Landing-page',
  },
  {
    title: 'Nexora',
    category: '3D Web Concept',
    excerpt: 'A bold 3D concept showcasing product visuals in immersive layouts.',
    description:
      'Nexora highlights futuristic interface composition by combining 3D visual assets with clean text hierarchy and intuitive section transitions.',
    tags: ['3D', 'UI/UX', 'Futuristic'],
    techStack: ['Spline', 'Figma',],
    features: ['Immersive hero scenes', 'Balanced typography', 'Directional visual flow', 'Interaction Prototyping'],
    image: image10,
    link: 'https://www.behance.net/gallery/234986329/Nexora-ai-3d-design',
  },
  {
    title: 'Virtara',
    category: '3D Product Showcase',
    excerpt: 'A high-impact 3D presentation designed for product-led storytelling.',
    description:
      'Virtara focuses on premium product showcasing using layered visual depth, smooth section pacing, and a consistent futuristic UI direction.',
    tags: ['3D', 'Showcase', 'Product'],
    techStack: ['Spline', 'Figma'],
    features: ['Depth-oriented visuals', 'Premium layout hierarchy', 'Interaction Prototyping'],
    image: image11,
    link: 'https://www.behance.net/gallery/234988367/Virtara-3d-design',
  },
  {
    title: 'Cryenix',
    category: 'Landing Page Project',
    excerpt: 'Sleek landing page concept with energetic branding and focused UX.',
    description:
      'Cryenix is designed to communicate innovation through a sleek visual system, balanced copy blocks, and modern interaction ideas tailored for first impressions.',
    tags: ['Landing', 'Brand', 'UX'],
    techStack: ['Figma', 'Spline'],
    features: ['Strong first-screen impact', 'Brand-led component styles', 'Interaction Prototyping'],
    image: image12,
    link: 'https://www.behance.net/gallery/235035961/Cryenix-Landing-page',
  },
  {
    title: 'Fortrez',
    category: 'Cypto-Based Charity Website',
    excerpt: 'Identity-focused website with modern conversion-first UI patterns.',
    description:
      'Fortrez is a modern digital platform designed to present cybersecurity services through a smooth conversion-focused experience with clean visual hierarchy and accessible interactions.',
    tags: ['Web', 'UI Design', 'Landing'],
    techStack: ['Vue', 'Nuxt', 'TypeScript', 'Tailwind CSS', 'REST APIs'],
    features: ['Responsive sections', 'Conversion-focused hero', 'Reusable UI blocks', 'Fast loading visuals'],
    image: image5,
    link: 'https://www.fortrez.io/',
  },
  {
    title: 'HR Solutions',
    category: 'Business Service Website',
    excerpt: 'A polished service platform with clear journeys for talent and employers.',
    description:
      'HR Solutions presents recruiting and people-management services with engaging sections, strong visual storytelling, and clear calls to action for prospective clients.',
    tags: ['Web', 'Branding', 'Responsive'],
    techStack: ['Framer', 'Modern CSS'],
    features: ['Service discovery flow', 'Content-first layout', 'Lead capture CTAs', 'Mobile-first behavior'],
    image: image7,
    link: 'https://hrsolutions.framer.website/',
  },
];

const activeWork = ref(null);

const openWork = (work) => {
  activeWork.value = work;
};

const closeModal = () => {
  activeWork.value = null;
};

const handleEsc = (event) => {
  if (event.key === 'Escape' && activeWork.value) {
    closeModal();
  }
};

watch(activeWork, (work) => {
  document.body.style.overflow = work ? 'hidden' : '';
});

onMounted(() => {
  window.addEventListener('keydown', handleEsc);
});

onUnmounted(() => {
  window.removeEventListener('keydown', handleEsc);
  document.body.style.overflow = '';
});
</script>
