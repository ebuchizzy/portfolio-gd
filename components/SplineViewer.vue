<template>
    <div ref="splineContainer" class="absolute right-0 top-0 w-1/2 h-full pointer-events-none"></div>
  </template>
  
  <script setup>
  import { onMounted, ref } from 'vue'
  import { Application } from '@splinetool/runtime'
  
  const splineContainer = ref(null)
  const props = defineProps({
    url: {
      type: String,
      required: true
    }
  })
  
  onMounted(() => {
    if (splineContainer.value) {
      const spline = new Application(splineContainer.value)
      spline.load(props.url)
    }
  })
  </script>
  