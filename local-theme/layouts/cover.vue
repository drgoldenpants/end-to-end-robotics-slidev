<script setup lang="ts">
import { computed, useSlots } from 'vue'

const slots = useSlots()
const hasDefaultSlot = computed(() => !!slots.default)

const props = defineProps({
  institute: {
    type: String,
    default: 'Robotics Institute',
  },
  course: {
    type: String,
    default: '41118 AI in robotics',
  },
  topic: {
    type: String,
    default: 'k-Means and PCA',
  },
  author: {
    type: String,
    default: 'Gibson Hu',
  },
})
</script>

<template>
  <div class="slidev-layout cover w-full h-full relative overflow-hidden">
    <div class="absolute inset-0 z-0">
      <img src="/template/background_first_slide.jpg" class="w-full h-full object-cover" />
    </div>

    <div class="absolute inset-0 z-10 flex flex-col justify-center items-start pl-20 text-white font-bold h-full text-left"> 
      <div v-if="hasDefaultSlot" class="cover-slot">
        <slot />
      </div>
      <div v-else>
        <h1 class="text-6xl mb-4 font-extrabold tracking-tight text-left">{{ props.institute }}</h1>
        <div class="mt-8 space-y-4 text-left">
          <div class="text-4xl">{{ props.course }}</div>
          <div class="text-4xl">{{ props.topic }}</div>
          <div class="text-4xl mt-8">{{ props.author }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.slidev-layout.cover h1 {
  color: white;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.5); /* Optional: add text shadow for readability on image */
}
.slidev-layout.cover .cover-slot h1 {
  font-size: 3.75rem;
  line-height: 1;
  font-weight: 800;
  margin-bottom: 1rem;
  letter-spacing: -0.02em;
}

.slidev-layout.cover .cover-slot h2 {
  font-size: 2.25rem;
  line-height: 2.5rem;
  font-weight: 700;
  margin-top: 1.5rem;
}
</style>
