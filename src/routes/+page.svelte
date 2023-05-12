<script lang="ts">
	import { onMount } from 'svelte'
	import Pagination from '../components/Pagination.svelte'
	import CharacterCard from '../components/CharacterCard.svelte'
	import LoadingCharacterCard from '../components/LoadingCharacterCard.svelte'

	let paginationData: any = {}
	let starwarsCharacters: any[] = []

	const paginationHandler = async (direction: boolean) => {
		if (direction) {
			if (paginationData.next) {
				starwarsCharacters.length = 0
				try {
					const newPage = await fetch(paginationData.next)
					const page = await newPage.json()
					paginationData = page
					starwarsCharacters = page.results
				} catch (error) {
					console.log(error)
				}
			}
		}
		
		if (!direction) {
			if (paginationData.previous !== null) {
				starwarsCharacters.length = 0
				try {
					const newPage = await fetch(paginationData.previous)
					const page = await newPage.json()
					paginationData = page
					starwarsCharacters = page.results
				} catch (error) {
					console.log(error)
				}
			}
		}
	}

	onMount(async () => {
		try {
			const fetchStarWarsCharacters = await fetch('https://swapi.dev/api/people')
			const characters = await fetchStarWarsCharacters.json()
			starwarsCharacters = characters.results
			paginationData = characters
			console.log(paginationData)
		} catch (error) {
			console.log(error)
		}
	})
</script>

<section id="characters" class="flex flex-wrap gap-5 w-full">
	<Pagination {paginationHandler} {paginationData} />

	{#if starwarsCharacters.length > 0}
		{#each starwarsCharacters as char}
			<CharacterCard {char} />
		{/each}
	{:else}
		{#each Array(10) as _}
			<LoadingCharacterCard />
		{/each}
	{/if}

	<Pagination {paginationHandler} {paginationData} />
</section>
