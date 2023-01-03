<script>
	import PokeList from './PokeList.svelte'
	import PokeDetails from './PokeDetails.svelte'
	
	const promise = getPokemons();
	let selectedPokemon = null

	async function getPokemons() {
		const res = await fetch('https://pokeapi.co/api/v2/pokemon/?offset=0&limit=151');
		const json = await res.json();
		
		return json.results;
	}
	
	function LijstVisi() {
		document.getElementById('list-pkmn').style.display = 'inline';
	}

	const selectPokemon = ({ detail }) => {
		selectedPokemon = detail;
	}
</script>

<h1>
	Pok�dex
</h1>

<div>
	{#await promise}
  	Chargement du Pokédex...
	{:then pokemons}
		<PokeList pokemons={pokemons} on:selectPokemon={selectPokemon}  />
		<PokeList></PokeList>
		{#if selectedPokemon}
			<PokeDetails pokemon={selectedPokemon} />
		{:else}
			Selecteer een pokemon
			<button id="btnVisi" on:click="{() => LijstVisi()}" >
				Gen 1 Lijst
	</button>
		{/if}
	{:catch error}
  	Er is wat mis gegaan : {error.message}
	{/await}
</div>

<style>
	h1 {
		text-align: center;
	}
	div {
		display: flex;
	}
	#btnVisi {
		width: 80px;
		height: 60px;
		display: fixed;
	}
</style>