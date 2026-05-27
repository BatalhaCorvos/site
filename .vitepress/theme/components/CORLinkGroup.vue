<script lang="ts" setup>
import { useRoute } from 'vitepress';
import { computed, ref, watch } from 'vue';
import CORChevDown from '../icons/CORChevDown.vue';


const props = defineProps({
	base: {type: String, mandatory: true, default: () => '' },
	links: { type: Array<{href: String, label:String}>, mandatory: false, default: () => []}
})

const open = defineModel({default: false})
const route = useRoute()
const isSelected = computed( () =>  route.path.match(props.base + '.*' ) != null )

watch(route, () => open.value = false)

</script>

<template>
	<div class="relative">
	<button 
	:class="isSelected ? 'font-bold' : ''"
	class="peer cursor-pointer text-lg flex gap-x-1 items-center" >
		<slot></slot> <CORChevDown class="size-4"></CORChevDown>
	</button>
	<div class="hover:flex ring ring-gray-600 hidden opacity-0 hover:opacity-100 peer-hover:opacity-100 peer-hover:flex  px-4 p-2 rounded-sm flex-col left-1/2 -translate-x-1/2 duration-500 transition-all absolute  bg-zinc-900/90">
		<a v-for="l of links" :href="props.base + l.href">
			{{ l.label }} 
		</a>
		</div>
	</div>
</template>
