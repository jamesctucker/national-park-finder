<script>
	import Header from './components/Header.svelte'
	import ParksList from './components/ParksList.svelte'
</script>

<main>
	<Header />
	<ParksList />
</main>

<style>
	main {
		text-align: center;
		max-width: 240px;
		margin: 0 auto;
		height: 100%;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>