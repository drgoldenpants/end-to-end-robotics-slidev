<template>
	<footer class="absolute bottom-0 left-0 right-0 flex text-center text-white pointer-events-auto z-50 text-2xl font-bold">
		<div class="flex-grow p-2 text-left pl-4 flex items-center" style="background:#cccccc">
			<span>UTS</span>
			<span v-if="renderedFootnote" class="mx-5 font-bold">|</span>
			<span v-html="renderedFootnote"></span>
		</div>
		<div class="flex-none p-2 text-right pr-4" style="background:#cccccc">
			{{ $slidev.nav.currentPage }} /
			<SlidesTotal />
		</div>
	</footer>
</template>

<script setup lang="ts">
import SlidesTotal from "@slidev/client/builtin/SlidesTotal.vue";
import MarkdownIt from 'markdown-it'
import { computed } from 'vue'
import { useNav } from '@slidev/client'

const { currentSlideRoute } = useNav()
const md = new MarkdownIt({ html: true, linkify: true, breaks: true })
const renderedFootnote = computed(() => {
	const footnote = currentSlideRoute.value.meta?.slide?.frontmatter?.footnote
	if (!footnote) return ''
	// Ensure footnote is a string before rendering
	return md.renderInline(String(footnote))
})
</script>
