<template>
    <footer class="relative isolate overflow-hidden bg-[#000716] py-8 text-center text-white">
      <div class="pointer-events-none absolute inset-0 bg-[radial-gradient(circle_at_top_center,rgba(255,255,255,0.08),transparent_24%),linear-gradient(160deg,#000512_12%,#020a18_52%,#050d1a_100%)]"></div>
      <div class="pointer-events-none absolute inset-0 opacity-[0.04] [background-image:linear-gradient(rgba(255,255,255,0.26)_1px,transparent_1px),linear-gradient(90deg,rgba(255,255,255,0.26)_1px,transparent_1px)] [background-size:84px_84px]"></div>
      <div class="relative z-10">
        <h3 class="mb-2 text-xl font-semibold">Chukwuebuka Akpuofoba</h3>
        <p>Copyright @{{ currentYear }} <a href="#" class="font-semibold text-primary">CEA</a>. All Rights Reserved.</p>
      </div>
    </footer>
  </template>
  
  <script setup>
  const currentYear = new Date().getFullYear();
  </script>
