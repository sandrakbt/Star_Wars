<script>
	import { onMount } from 'svelte';
  export let url;

  let person;

	async function update() {
		person = await getPerson(url);
    console.log(person)
    person.planet = await fetch(person.properties.homeworld).then(r => r.json()).then(r=>r.result)
  }
  
  $: update(url)

	function getPerson(url) {
		return fetch(url)
      .then(res => res.json())
			.then(data => data.result)
  }
</script>

<main>
  {#if person}
  <h2 class="name">{person.properties.name}</h2>
  <p class="planet"><span class="span">Gender:</span> {person.properties.gender}</p>
  <p class="planet"><span class="span">Planet:</span> {person.planet?.properties.name}</p>
  <p class="planet"><span class="span">Height [cm]:</span> {person.properties.height}</p>
  <p class="planet"><span class="span">Eye color:</span> {person.properties.eye_color}</p>
  <p class="planet"><span class="span">Skin color:</span> {person.properties.skin_color}</p>

  {/if}
</main>

<style>
	.name {
    color: yellow;
  }
  .span { 
    color: white;
    font-weight: bolder;
  }
  .planet {
    color: white;
  }
</style>
