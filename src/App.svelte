<script>
import { onMount } from 'svelte';

let photos = [];

let BASE_URL = "https://jsonplaceholder.typicode.com/";
let END_POINT = "photos?_limit=20";

onMount(async () => {
	const res = await fetch(`${BASE_URL+END_POINT}`);
	photos = await res.json();
});
</script>

<main>
	<h1>Ali Ergüç - Svelte Example Component</h1>
	<p>Örnek Fotoğraf Albümü</p>
	<div class="photos">
		{#each photos as photo}
			<figure>
				<img src={photo.thumbnailUrl} alt={photo.title}>
				<figcaption>{photo.title}</figcaption>
			</figure>
		{:else}			
			<p>Yükleniyor...</p>
		{/each}
	</div>
	
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	.photos {
		width: 100%;
		display: grid;
		grid-template-columns: repeat(5, 1fr);
		grid-gap: 8px;
	}

	figure, img {
		width: 100%;
		margin: 0;
	}
	h1 {
		color: #7700ff;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>