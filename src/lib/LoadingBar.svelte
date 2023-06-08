<script lang="ts">
	import { navigating } from '$app/stores';
	import { onMount } from 'svelte';

	export let loading: HTMLDivElement;

	onMount(() => {
		navigating.subscribe((value) => {
			if (value) {
				loading.classList.add('on');
			} else {
				loading.classList.add('done');
				setTimeout(() => {
					loading.classList.remove('on');
					loading.classList.remove('done');
				}, 1000);
			}
		});
	});
</script>

<div class="fixed top-0 left-0 right-0 w-full h-[4px] z-50">
	<div bind:this={loading} class="loading w-0 bg-sky-500 h-full" />
</div>

<style>
	.loading {
		width: 0%;
		opacity: 1;
		transition: none;
	}
	:global(.loading.on) {
		transition: width 2s 0s linear;
		width: 100%;
	}
	:global(.loading.done) {
		transition: width 0.1s 0s linear, opacity 0.5s 0.5s linear;
		opacity: 0;
	}
</style>
