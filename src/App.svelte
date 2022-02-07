<script>
	export let name;
  const sate = {
    url: 'https://satdash.wpengine.com/wp-json/wp/v2/satellites?count=2'
  }
  let sats = []
  const saludos = {
    eng: 'hello',
    spa: 'hola',
    gua: "mba'eichapa"
  }

  function getSats() {
    fetch(sate.url)
    .then( res => res.json())
    .then( data => sats = data)
  }

  let promise = getSats();

	function handleClick() {
		// promise = getSats();
    // promise = Object.entries(promise);
    console.log(sats);
    // const showSats = document.querySelector('ul')
    // const sat = document.createElement('li')
	}

</script>

<main>
	<h1>{saludos.spa + ' ' + name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
  <button on:click={handleClick}>
    Load Table
  </button>

  <ul>
    {#each sats as sat}
    <li>Sat ID: {sat.id}</li>
    {/each}
  </ul>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
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