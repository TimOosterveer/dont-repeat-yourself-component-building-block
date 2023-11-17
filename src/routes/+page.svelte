<script>
  export let data;
	import { onMount } from 'svelte';

  console.log(data);

  let selected = ['makkelijk', 'uitdagend'];
	const onderhouds = ['makkelijk', 'uitdagend	'];
	let filteredWorkshops = data.stekjes // Data van de workshops in filteredWorkshops
	
	console.log(filteredWorkshops)
	function filterWorkshops() {
		if (selected) {
			filteredWorkshops = stekjes.onderhoud.filter((ond) => {
				console.log(filteredWorkshops)
				return ond.onderhoud.toLowerCase().includes(selected.toLowerCase());
			});
		} else {
			filteredWorkshops = data.stekjes;
		}
	}
</script>


<form on:submit|preventDefault={filterWorkshops}>
	<label for="month">Selecteer maand:</label>
	<select id="month" bind:value={selected} on:change={filterWorkshops}>
		<option value="">alle</option>
		{#each onderhouds as month}
			<option value={month}>{month}</option>
		{/each}
	</select>
</form>

<section class="wrapper">
	{#each filteredWorkshops as stekje}
		<a href={stekje.slug}>
			<article>
				<img src={stekje.fotos[0].url} alt="foto van {stekje.naam}" />
				<div>
					<h3>{stekje.naam}</h3>
					<p>{stekje.onderhoud}</p>
				</div>
			</article>
		</a>
	{/each}
</section>

<style>
	select {
		display: flex;
		flex-direction: column;
		width: 10rem;
		padding: 0.5rem;
		border-radius: 0;
		border: 2px solid #4d7141;
	}

	select:focus {
		border: 3px solid rgb(17, 84, 255);
	}

	.wrapper {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		gap: 1rem;
		margin: 2rem;
		justify-content: center;
		align-items: center;
	}

	.wrapper a {
		text-decoration: none;
		padding-bottom: 2rem;
	}

	article {
		display: flex;
		flex-direction: column;
		width: 195px;
		height: 266px;
		border-radius: 7px;
		box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
		position: relative;
	}

	article img {
		width: 100px;
		position: absolute;
		height: 266px;
		width: 195px;
		top: 0;
		left: 0;
		border-radius: 7px;
	}

	article div {
		width: 195px;
		height: 89px;
		border-bottom-left-radius: 7px;
		border-bottom-right-radius: 7px;
		background-color: #0d350cde;
		color: whitesmoke;
		top: 177px;
		position: relative;
	}

	article div h3 {
		padding: 0.5rem;
		font-size: 17px;
	}

	article:hover {
		top: -10px;
	}
</style>



