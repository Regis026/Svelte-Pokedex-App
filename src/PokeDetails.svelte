<link rel="stylesheet" href="https://justingolden.me/pokemon-types-css/types.min.css">

<script>
	export let pokemon
	let promise
	$: promise = getPokemon(pokemon.url)
	
	async function getPokemon(url) {
		const res = await fetch(pokemon.url);
		return await res.json();
	}
</script>

<div>
	
  {#await promise}
    Chargement de {pokemon.name}&
  {:then pokemonDetails}
		
    <h2>{pokemonDetails.name}</h2>
		{#each pokemonDetails.types as type}
			<span style="margin: 3px;" class="type {type.type.name}"></span>
		{/each}
	<br>
	<br>
    <img src={pokemonDetails.sprites.front_default} alt={pokemonDetails.name} />
		<img src={pokemonDetails.sprites.front_shiny} alt={pokemonDetails.name} />
		<h2>Abilities:</h2>
		{#each pokemonDetails.abilities as ability}
		<h2>● {ability.ability.name}</h2>
		{/each}
		<h2>Base Stats:</h2>
		{#each pokemonDetails.stats as stat}
		<h2>● {stat.stat.name}: {stat.base_stat}</h2>
		{/each}
  {:catch error}
    Er is wat mis gegaan : {error.message}
  {/await}
</div>