<script lang="ts">
	import { slide } from 'svelte/transition';
	import { getContext } from 'svelte';
	import { getAccordionOptions } from './context';

	export let open = false;

	const componentId = crypto.randomUUID();
	const { colapse, activeComponentId } = getAccordionOptions();

	function setActive() {
		$activeComponentId = componentId;
	}

	function toggleOpen() {
		open = !open;
	}

	function handleClick() {
		colapse ? setActive() : toggleOpen();
	}

	$: open && colapse && setActive();
	$: isActive = $activeComponentId === componentId;
	$: isOpen = colapse ? isActive : open;
</script>

<div class="accordion-item">
	<button
		on:click={handleClick}
		class="accordion-toggle"
		aria-expanded={isOpen}
		aria-controls="accordion-{componentId}"
	>
		<div class="accordion-title">
			<slot name="title" />
		</div>

		<div class="accordion-caret" class:open={isOpen} class:close={!isOpen}>👉️</div>
	</button>

	{#if isOpen}
		<div
			transition:slide|local
			class="accordion-content"
			role="region"
			aria-hidden={!isOpen}
			aria-labelledby="accordion-{componentId}"
		>
			<slot name="content" />
		</div>
	{/if}
</div>

<style>
	.accordion-toggle {
		display: flex;
		justify-content: space-between;
		width: 100%;
		padding: var(--accordion-padding, 1rem);
		color: var(--accordion-color, inherit);
		font: inherit;
		font-weight: 600;
		border: none;
		background: none;
		cursor: pointer;
		border-radius: var(--accordion-radius, 4px);
		transition: background-color 0.1s ease;
	}
	.accordion-toggle:hover {
		background-color: var(--accordion-background, hsl(220 20% 20%));
	}

	.accordion-content {
		padding: var(--accordion-padding, 1rem);
	}

	.open {
		transform: rotate(90deg);
		transition: transform 0.3s ease;
	}

	.close {
		transform: rotate(0deg);
		transition: transform 0.3s ease;
	}
</style>
