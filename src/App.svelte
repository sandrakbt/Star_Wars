<script>
	import { onMount } from 'svelte';
	import Person from './Person.svelte';

	let people = [];

	let pageNumber = 1
	onMount(async () => {
		people = await getPeople(pageNumber);
		console.log(people)
	});

	async function changePage (next) {
		pageNumber += next 
		people = await getPeople(pageNumber)
		console.log(people)
	}

	function getPeople(page) {
		return fetch(`https://www.swapi.tech/api/people?page=${page}&limit=10`)
			.then(res => res.json())
			.then(data => data.results)
	}
</script>

<div class="wrapper">
	<header class="header">
		<h1 class="title">
			<img src="Star_Wars_Logo.svg.png" alt="star wars logo" width="350px">
		</h1>
		<p class="text">Characteristics of some characters from the movies:</p>
	</header>
	<div>
		<button class="button1" on:click = {()=>changePage(-1)}>Back</button>
		<button class="button2" on:click = {()=>changePage(1)}>Next</button>
	</div>
	<ul>
		{#each people as person, i}
			<li>
				<Person url={person.url} />
			</li>
		{/each}
	</ul>
</div>

<style>
.title {
	color: gold;
	font-size: xx-large;
	margin-top: 0px;
}
.text {
	color: white;
	font-size: x-large;
}

.button1 {
	background-color:tomato;
	border-radius: 8px;
	border:none;
	font-weight:bold;
}

.button2 {
	background-color:yellow;
	border-radius: 8px;
	border: none;
	font-weight: bold;
}
</style>