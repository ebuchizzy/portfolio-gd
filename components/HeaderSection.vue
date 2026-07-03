<template>
  <header class="fixed inset-x-0 top-0 z-50">
    <div class="px-4 pt-4 sm:px-6 md:px-10">
      <div class="mx-auto w-full max-w-6xl transition-all duration-300">
        <div
          :class="[
            'relative overflow-hidden rounded-full border px-4 py-3 shadow-[0_18px_40px_rgba(0,0,0,0.22)] backdrop-blur-xl transition-all duration-300 sm:px-6 lg:px-8',
            isSticky || isMenuOpen
              ? 'border-white/16 bg-[#000716]/90'
              : 'border-white/14 bg-[#000716]/85'
          ]"
        >
          <div class="pointer-events-none absolute inset-0 bg-[linear-gradient(120deg,rgba(58,108,244,0.18),transparent_35%,transparent_65%,rgba(255,255,255,0.08))]"></div>

          <div class="relative flex items-center justify-between gap-4 lg:hidden">
            <NuxtLink
              to="/"
              class="inline-flex h-11 w-11 items-center justify-center rounded-full border border-white/20 bg-white/10 backdrop-blur-sm sm:text-2xl font-semibold uppercase text-white transition-colors duration-300 hover:border-primary/60 hover:bg-primary/15"
              @click.prevent="goHome" 
            >
              CEA
            </NuxtLink>

            <button
              type="button"
              @click.stop="toggleMenu"
              :aria-expanded="isMenuOpen"
              aria-label="Toggle navigation menu"
              class="relative z-[60] flex h-11 w-11 items-center justify-center rounded-full border border-white/20 bg-white/10 backdrop-blur-sm transition-colors duration-300 focus:outline-none"
        >
          <span
            :class="[
              'absolute h-0.5 w-5 transform rounded-full bg-white transition-all duration-300 ease-in-out',
              isMenuOpen ? 'translate-y-0 rotate-45' : '-translate-y-1.5'
            ]"
          ></span>
          <span
            :class="[
              'absolute h-0.5 w-5 transform rounded-full bg-white transition-all duration-300 ease-in-out',
              isMenuOpen ? 'translate-y-0 -rotate-45' : 'translate-y-1.5'
            ]"
          ></span>
            </button>
          </div>

          <div class="relative hidden items-center justify-between gap-6 lg:flex">
            <nav class="flex items-center gap-2">
              <a
                v-for="link in leftLinks"
                :key="link.to"
                :href="link.to"
                @click="handleLinkClick(link.to)"
                :class="desktopLinkClass(link.to)"
              >
                {{ link.text }}
              </a>
            </nav>

            <NuxtLink
              to="/"
              class="inline-flex h-14 min-w-[112px] items-center justify-center rounded-full border border-white/12 bg-white/6 px-7 text-sm font-semibold uppercase tracking-[0.32em] text-white transition-all duration-300 hover:border-primary/60 hover:bg-primary/15"
              @click.prevent="goHome"
            >
              CEA
            </NuxtLink>

            <nav class="flex items-center gap-2">
              <a
                v-for="link in rightLinks"
                :key="link.to"
                :href="link.to"
                @click="handleLinkClick(link.to)"
                :class="desktopLinkClass(link.to)"
              >
                {{ link.text }}
              </a>
            </nav>
          </div>
        </div>

        <Transition
          enter-active-class="transition duration-300 ease-out"
          enter-from-class="-translate-y-4 opacity-0"
          enter-to-class="translate-y-0 opacity-100"
          leave-active-class="transition duration-200 ease-in"
          leave-from-class="translate-y-0 opacity-100"
          leave-to-class="-translate-y-3 opacity-0"
        >
          <div v-if="isMenuOpen" class="relative lg:hidden">
            <button
              type="button"
              aria-label="Close navigation menu"
              class="fixed inset-0 top-[88px] z-30 bg-transparent"
              @click="closeMenu"
            ></button>

            <nav class="relative z-40 mx-2 mt-3 overflow-hidden rounded-[30px] border border-white/15 bg-[#000716]/95 p-3 shadow-[0_24px_50px_rgba(0,0,0,0.32)] backdrop-blur-xl">
              <a
                v-for="link in navLinks"
                :key="`mobile-${link.to}`"
                :href="link.to"
                @click="handleLinkClick(link.to)"
                :class="[
                  'mb-2 flex items-center justify-between rounded-full px-5 py-3 text-sm font-medium tracking-[0.12em] transition-all duration-300 last:mb-0',
                  activeLink === link.to
                    ? 'bg-primary text-white shadow-[0_12px_28px_rgba(58,108,244,0.34)]' // Active link (already white)
                    : 'bg-white/[0.06] text-white hover:bg-white/[0.1]' // Inactive link changed to text-white
                ]"
              >
                <span>{{ link.text }}</span>
                <span class="text-base leading-none text-white/70">&bull;</span>
              </a>
            </nav>
          </div>
        </Transition>
      </div>
    </div>
  </header>
</template>

<script setup>
import { computed, onMounted, onUnmounted, ref } from 'vue';

const isSticky = ref(false);
const isMenuOpen = ref(false);
const activeLink = ref('#main');

/**
 * Lock background scroll while the mobile menu is open.
 * Uses overflow only (no position:fixed on #__nuxt/body) so the current section
 * stays painted behind the menu instead of a blank viewport.
 */
const setMenuScrollLock = (locked) => {
  if (typeof document === 'undefined') return;
  const { documentElement: html, body } = document;
  if (locked) {
    html.style.overflow = 'hidden';
    body.style.overflow = 'hidden';
  } else {
    html.style.overflow = '';
    body.style.overflow = '';
  }
};

const navLinks = [
  { text: 'Home', to: '#main' },
  { text: 'About', to: '#about' },
  { text: 'Skills', to: '#skills' },
  { text: 'Services', to: '#services' },
  { text: 'Work', to: '#work' },
  { text: 'Contact', to: '#contact' }
];

const leftLinks = computed(() => navLinks.slice(0, 3));
const rightLinks = computed(() => navLinks.slice(3));

const closeMenu = () => {
  isMenuOpen.value = false;
  setMenuScrollLock(false);
};

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
  setMenuScrollLock(isMenuOpen.value);
};

const handleScroll = () => {
  isSticky.value = window.scrollY > 12;
};

const goHome = () => {
  activeLink.value = '#main';
  closeMenu();

  const el = document.getElementById('main');
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' });
    return;
  }

  window.scrollTo({ top: 0, behavior: 'smooth' });
};

const handleLinkClick = (linkTo) => {
  activeLink.value = linkTo;
  closeMenu();
};

const desktopLinkClass = (linkTo) => [
  'rounded-full px-5 py-3 text-sm font-medium tracking-[0.12em] transition-all duration-300',
  activeLink.value === linkTo
    ? 'bg-primary text-white shadow-[0_12px_28px_rgba(58,108,244,0.34)]'
    : 'text-white hover:bg-primary hover:text-white hover:shadow-[0_12px_28px_rgba(58,108,244,0.28)]'
];

onMounted(() => {
  handleScroll();
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
  isMenuOpen.value = false;
  setMenuScrollLock(false);
});
</script>
