<script>
	import { onMount } from 'svelte';
	import Person from './Person.svelte';

	let people = [];

	onMount(async () => {
		people = await getPeople(2);
		console.log(people)
	});

	function getPeople(page) {
		return fetch(`https://www.swapi.tech/api/people?page=${page}&limit=10`)
			.then(res => res.json())
			.then(data => data.results)
	}
</script>

<main>
	{#each people as person, i}
		<Person url={person.url} />
	{/each}
	<h1></h1>
	<p></p>
</main>

<style>
	
</style>