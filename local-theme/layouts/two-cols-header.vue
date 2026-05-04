
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
  <div class="slidev-layout two-cols-header w-full h-full" :class="layoutClass">
    <div class="col-header">
      <h1 v-if="header">{{ header }}</h1>
      <slot />
    </div>

    <div class="col-left" :class="[props.class, `text-${props.textAlign}`, 'flex', 'flex-col', 'h-full', alignClass]">
      <div v-if="$slots['left-center']" class="flex flex-col items-center h-full text-center" :class="alignClass">
        <slot name="left-center" />
      </div>
      <div v-else-if="props.textAlign == 'center'" class="flex flex-col items-center h-full text-center" :class="alignClass">
        <slot name="left" />
      </div>
      <slot name="left" v-else />
    </div>
    <div class="col-right" :class="[props.class, `text-${props.textAlign}`, 'flex', 'flex-col', 'h-full', alignClass]">
      <div v-if="$slots['right-center']" class="flex flex-col items-center h-full text-center" :class="alignClass">
        <slot name="right-center" />
      </div>
      <div v-else-if="props.textAlign == 'center'" class="flex flex-col items-center h-full text-center" :class="alignClass">
        <slot name="right" />
      </div>
      <slot name="right" v-else />
    </div>
    <div class="col-bottom" :class="[props.class, `text-${props.textAlign}`]">
      <div v-if="props.textAlign == 'center'" class="flex flex-col items-center justify-center h-full text-center">
        <slot name="bottom" />
      </div>
      <slot name="bottom" v-else />
    </div>
  </div>
</template>

<style scoped>
.two-cols-header {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: auto 1fr auto;
}

.col-header {
  grid-area: 1 / 1 / 2 / 3;
}
.col-left {
  grid-area: 2 / 1 / 3 / 2;
}
.col-right {
  grid-area: 2 / 2 / 3 / 3;
}
.col-bottom {
  align-self: end;
  grid-area: 3 / 1 / 3 / 3;
}
</style>

