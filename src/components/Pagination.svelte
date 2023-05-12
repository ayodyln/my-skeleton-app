<script lang="ts">
	export let paginationHandler: any, paginationData: any
</script>

<section id="pagination" class="w-full flex justify-center items-center gap-4">
	{#if paginationData.previous}
		<button on:click={() => paginationHandler(false)} type="button" class="btn-icon variant-filled"
			>←</button
		>
	{/if}
	<span class="text-xl">
		{#if !paginationData.previous && paginationData.next}
			1
		{/if}

		{#if paginationData.previous && paginationData.next}
			{paginationData.previous.slice(-1) * 1 + 1}
		{/if}

		{#if paginationData.previous && !paginationData.next}
			{paginationData.previous.slice(-1) * 1 + 1}
		{/if}
	</span>
	{#if paginationData.next}
		<button on:click={() => paginationHandler(true)} type="button" class="btn-icon variant-filled"
			>→</button
		>
	{/if}
</section>
