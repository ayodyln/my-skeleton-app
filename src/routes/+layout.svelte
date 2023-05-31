<script lang="ts">
	// The ordering of these imports is critical to your app working properly
	import '@skeletonlabs/skeleton/themes/theme-skeleton.css'
	// If you have source.organizeImports set to true in VSCode, then it will auto change this ordering
	import '@skeletonlabs/skeleton/styles/skeleton.css'
	// Most of your app wide CSS should be put in this file
	import { computePosition, autoUpdate, offset, shift, flip, arrow } from '@floating-ui/dom'
	import '../app.postcss'
	import { AppShell, AppBar } from '@skeletonlabs/skeleton'

	import { storePopup } from '@skeletonlabs/skeleton'

	export const prerender = true

	storePopup.set({ computePosition, autoUpdate, offset, shift, flip, arrow })
</script>

<!-- App Shell -->
<AppShell>
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar>
			<svelte:fragment slot="lead">
				<div>
					<strong class="text-xl uppercase">StarWars Characters</strong>
					<p>SvelteKit // SkeletonUI</p>
				</div>
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<!-- Page Route Content -->
	<section class="max-w-5xl m-auto my-4">
		<slot />
	</section>
</AppShell>
