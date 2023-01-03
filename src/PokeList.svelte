<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();
	
	export let pokemons = []
	
	const handlePokemonClick = (pokemon) => {
		dispatch('selectPokemon', pokemon)
		document.body.scrollIntoView();
	}
</script>

<ul id="list-pkmn" style="display: none">
	{#each pokemons as pokemon}
	<div>
		<button on:click="{() => handlePokemonClick(pokemon)}" >
			{pokemon.name}
		</button>
	</div>
	{/each}
</ul>