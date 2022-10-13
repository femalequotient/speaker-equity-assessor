<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	export let href = '';
	export let primaryLabel = '';
	export let secondaryLabel = '';

	enum ContainerType {
		LINK,
		SPAN
	}
	let container = ContainerType.SPAN;
	if (href !== '') {
		container = ContainerType.LINK;
	}

	const dispatchClick = (event: Event) => {
		dispatch('click', event);
	};
</script>

{#if container === ContainerType.LINK}
	<a {href} on:click={dispatchClick}>
		<div class="button">
			{#if primaryLabel}
				<div class="primaryLabel">{primaryLabel}</div>
			{/if}
			{#if secondaryLabel}
				<div class="secondaryLabel">{secondaryLabel}</div>
			{/if}
		</div>
	</a>
{:else}
	<span on:click={dispatchClick}>
		<div class="button">
			{#if primaryLabel}
				<div class="primaryLabel">{primaryLabel}</div>
			{/if}
			{#if secondaryLabel}
				<div class="secondaryLabel">{secondaryLabel}</div>
			{/if}
		</div>
	</span>
{/if}

<style>
	a {
		text-decoration: none;
	}
	.button {
		background-color: var(--button-background-color, #ffffff);
		color: var(--button-color, #000000);
		font-weight: bold;
		text-transform: uppercase;
		cursor: pointer;
		padding: 12px 30px;
		text-align: center;
		display: flex;
		flex-direction: column;
	}
	.button:hover {
		background-color: var(--button-hover-background-color, #cccccc);
	}
	.primaryLabel {
		font-size: 1em;
	}
	.secondaryLabel {
		margin-top: 7px;
		font-size: 0.8em;
	}
</style>
