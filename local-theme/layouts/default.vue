<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  class: {
    type: String,
  },
  layoutClass: {
    type: String,
  },
  textAlign: {
    type: String,
    default: 'left',
  },
  header: {
    type: String,
  },
  verticalAlign: {
    type: String,
    default: 'top',
  },
})

const alignClass = computed(() => {
  if (props.verticalAlign === 'center') return 'justify-center'
  if (props.verticalAlign === 'bottom') return 'justify-end pb-12'
  return 'justify-start'
})
</script>

<template>
  <div class="slidev-layout default w-full h-full" :class="[layoutClass, props.class]">
    <div class="col-header">
      <h1 v-if="header">{{ header }}</h1>
    </div>

    <div class="col-content flex flex-col h-full" :class="[`text-${props.textAlign}`, alignClass]">  
      <div v-if="props.textAlign == 'center'" class="flex flex-col items-center h-full text-center" :class="alignClass">
         <slot />
      </div>
      <slot v-else />
    </div>
  </div>
</template>

<style scoped>
.default {
  display: grid;
  grid-template-rows: auto 1fr;
}
.col-header {
  grid-row: 1;
}
.col-content {
  grid-row: 2;
  overflow: hidden;
}
</style>
