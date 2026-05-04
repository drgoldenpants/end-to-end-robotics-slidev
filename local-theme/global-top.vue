<template>
	<!-- <Frankfurt /> -->
	<CustomInfoLine v-if="($slidev.configs.infoLine ?? true) && $slidev.nav.currentLayout !== 'cover' && $slidev.nav.currentLayout !== 'section'" />
	<img v-if="$slidev.nav.currentLayout !== 'cover' && $slidev.nav.currentLayout !== 'section'" src="/template/UTS_logo.png" class="absolute top-4 right-4 w-15" />
</template>

