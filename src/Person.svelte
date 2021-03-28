<script>
	import { onMount } from 'svelte';
  export let url;

  let person;

	onMount(async () => {
		person = await getPerson(url);
    console.log(person)
    person.planet = await fetch(person.properties.homeworld).then(r => r.json()).then(r=>r.result)
	});

	function getPerson(url) {
		return fetch(url)
      .then(res => res.json())
			.then(data => data.result)
	}
</script>

<main>
  {#if person}
	<h2>{person.properties.name}</h2>
  <p>{person.properties.eye_color}</p>
  <p>{person.planet?.properties.name}</p>
  {/if}
</main>

<style>
	h2 {
    color: red;
  }
</style>
