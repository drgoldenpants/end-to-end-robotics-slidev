<script setup lang="ts">


const props = defineProps({
  number: {
    type: [String, Number],
    default: '1',
  },
  sectionTitle: {
    type: String,
    default: 'Title',
  },
  label: {
    type: String,
    default: '',
  },
  subtitle: {
    type: String,
    default: '',
  },
  image: {
    type: String,
    default: '/template/UTS_illustration.png',
  },
})
const resolveAssetUrl = (url: string) => url.startsWith("/") ? import.meta.env.BASE_URL + url.slice(1) : url;
</script>

<template>
  <div class="slidev-layout section-frame w-full h-full relative overflow-hidden bg-gray-100 flex items-center">
    
    <!-- Image (Left Side) -->
    <div class="absolute inset-0 z-10 w-full h-full pointer-events-none flex items-center justify-start">
      <img :src="resolveAssetUrl(props.image)" class="object-contain" style="height: 66.7%; margin-left: 5%; object-position: left center;" />
    </div>

    <!-- Number Circle (Blue) -->
    <div class="absolute z-20 rounded-full bg-[#0F4BEB] text-white flex items-center justify-center font-bold shadow-none"
         style="
            width: 12vh; 
            height: 12vh; 
            left: 40%; 
            top: 25%;
            transform: translate(-50%, -50%);
         ">
         <!-- Font size increased to match -->
        <span style="font-size: 8vh; line-height: 1;">
          {{ props.number < 10 ? '0' + props.number : props.number }}
        </span>
    </div>

    <!-- Right Side Content -->
    <div class="absolute z-30 flex flex-col justify-center h-full pl-8"
         style="
            left: 45%; 
            width: 50%;
            top: 0;
         ">
        
        <div class="text-[#0F4BEB] font-bold leading-tight">
            <h1 class="text-6xl !m-0 !p-0 leading-none">{{ props.sectionTitle }}</h1>
        </div>
        <div v-if="props.label || props.subtitle" class="text-gray-800 text-2xl leading-relaxed mt-2">
            <span v-if="props.label !== ''" class="font-bold text-black">{{ props.label }}:</span> 
            <span class="ml-2 font-normal">{{ props.subtitle }}</span>
        </div>

    </div>



  </div>
</template>