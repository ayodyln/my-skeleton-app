<script lang="ts">
	import { ProgressRadial } from '@skeletonlabs/skeleton'

	export let char: any

	const getCharID = (url: string) => url.split('/').filter(Boolean).pop()

	const birthYearString = (date: string) => {
		if (date === 'unknown') return date
		return `${date.slice(0, -3)} ${date.slice(-3)}`
	}

	const getSpecies = async (endpoint: any) => {
		if (endpoint.length > 0) {
			try {
				const species = await fetch(endpoint[0])
				const res = await species.json()
				return res.name
			} catch (error) {
				console.log(error)
				return ''
			}
		} else return 'Human'
	}

	const getHomeWorld = async (homeworld: string) => {
		if (homeworld) {
			try {
				const getWorld = await fetch(homeworld)
				const res = await getWorld.json()
				return res.name
			} catch (error) {
				console.log(error)
			}
		}
	}
</script>

<section class="card max-w-[49%] h-[250px] w-full relative card-hover">
	<div class="p-4 flex gap-4 ralative w-full h-full">
		<figure class="h-full max-h-[215px] w-1/3 rounded-lg overflow-hidden shadow-lg">
			<img
				src={`https://starwars-visualguide.com/assets/img/characters/${getCharID(char.url)}.jpg`}
				alt={char.name}
				class="w-auto h-full"
			/>
		</figure>

		<div class="w-2/3 h-full flex flex-col gap-3">
			<div id="name" class="h-fit bg-surface-900 p-2 rounded-lg shadow">
				<h1 class="aurabesh_name text-warning-500">{char.name}</h1>
				<h2 class="text-surface-500 text-xs">{char.name}</h2>
			</div>

			<div id="info" class="w-full grid grid-cols-2 gap-2">
				<div class="p-1 px-2 h-[44px] bg-surface-900 rounded-md">
					<p class="aurabesh_name w-fit text-sm">
						{char.mass} <span>kg</span>
					</p>
					<p class="text-surface-500 text-xs">{char.mass} kg</p>
				</div>

				<div class="p-1 px-2 h-[44px] bg-surface-900 rounded-md">
					<p class="aurabesh_name w-fit text-sm">
						{char.height / 100} <span>m</span>
					</p>
					<p class="text-surface-500 text-xs">{char.height / 100} m</p>
				</div>

				<div class="p-1 px-2 h-[44px] bg-surface-900 rounded-md">
					<p class="aurabesh_name w-fit text-sm">
						{char.gender === 'n/a' ? 'N/A' : char.gender}
					</p>
					<p class="text-surface-500 text-xs capitalize">
						{char.gender === 'n/a' ? 'No Gender' : char.gender}
					</p>
				</div>

				<div class="p-1 px-2 h-[44px] bg-surface-900 rounded-md">
					<p class="aurabesh_name w-fit text-sm">
						{birthYearString(char.birth_year)}
					</p>
					<p class="text-surface-500 text-xs capitalize">
						{birthYearString(char.birth_year)}
					</p>
				</div>

				<div class="p-1 px-2 h-[44px] bg-surface-900 rounded-md">
					{#await getSpecies(char.species)}
						<span class="w-full h-full flex justify-center items-center">
							<ProgressRadial width="w-6" value={undefined} />
						</span>
					{:then str}
						<p class="aurabesh_name w-fit text-sm">
							{str}
						</p>
						<p class="text-surface-500 text-xs">{str}</p>
					{/await}
				</div>

				<div class="p-1 px-2 h-[44px] bg-surface-900 rounded-md">
					{#await getHomeWorld(char.homeworld)}
						<span class="w-full h-full flex justify-center items-center">
							<ProgressRadial width="w-6" value={undefined} />
						</span>
					{:then str}
						<p class="aurabesh_name w-fit text-sm">
							{str}
						</p>
						<p class="text-surface-500 text-xs">{str}</p>
					{/await}
				</div>
			</div>
		</div>
	</div>
</section>

<style>
	.aurabesh_name {
		font-family: 'Aurabesh';
	}
</style>
