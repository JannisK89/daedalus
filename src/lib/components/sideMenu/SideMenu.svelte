<script context="module" lang="ts">
	export type SideMenuData = {
		header: string;
		content: string;
		next: string;
		previous: string;
		difficulty: string;
	};
</script>

<script lang="ts">
	import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import { showSideMenu } from '$lib/stores/sideMenu';
	import Tip from './Tip.svelte';
	import type { TipData } from './Tip.svelte';
	import Nav from './Nav.svelte';
	import Difficulty from './Difficulty.svelte';

	export let menuData: SideMenuData;
	export let tips: TipData[];
</script>

{#if $showSideMenu}
	<aside
		transition:fly|local={{ duration: 600, x: -2000, opacity: 0.8, easing: quintOut }}
		class="lg:w-4/12 bg-gray-100
		flex flex-col lg:mr-4 lg:fixed lg:top-0 lg:left-0  lg:block inset-0 lg:h-[calc(100vh-4.2rem)]  lg:my-16 lg:border-t-2 border-slate-200"
	>
		<Nav header={menuData.header} next={menuData.next} previous={menuData.previous} />
		<div class="m-6 lg:mx-10 flex flex-col flex-wrap ">
			<Difficulty difficulty={menuData.difficulty} />
			<div class="mb-4 lg:tracking-wide font-light">
				{@html menuData.content}
			</div>
			{#each tips as tip}
				<Tip tipData={tip} />
			{/each}
		</div>
	</aside>
{/if}
