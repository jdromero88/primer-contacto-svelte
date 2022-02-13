<script>
  import { onMount } from 'svelte'
  import Table from "./components/Table.svelte"
  import Button from "./components/Button.svelte"

	export let name;
  export let sats = []
  let originalSats = []
  let uniqueCountryOfLaunch = []
  let countryOfLaunch = []

  const sate = {
    url: 'https://satdash.wpengine.com/wp-json/wp/v2/satellites?count=2'
  }
  
  const saludos = {
    eng: 'hello',
    spa: 'hola',
    gua: "mba'eichapa"
  }

  const removeDuplicatesCoL = (array) => {
    console.log('remove duplicates Country of Launch')
    // remove duplicates duplicates values from array   
    if (array)
      uniqueCountryOfLaunch = [...new Set(array)]
  }

  onMount( () => {
    fetch(sate.url)
    .then( res => res.json())
    .then( data => {
      originalSats = [...data]
      sats = [...data]
      sats.forEach( sat => countryOfLaunch.push( sat.ag_meta.countryOfLaunch ) )
      removeDuplicatesCoL( countryOfLaunch )
    })
  })

  const changeName = () => {
    name = 'Jose'
    console.log(sats)
  }
	function handleClick() {
    console.log(sats)
	}

  const handleSearch = (e) => {
    let searchID = e.target.value
    const result = originalSats.filter(s => s.id.toString().includes(searchID))
    sats = [...result]
  }

  const filterBy = (e) => {
    let filter = e.target.value
    console.log(filter);
    const result = originalSats.filter( s => s.ag_meta.countryOfLaunch.includes(filter))
    sats = [...result]
  }
</script>

<main>
	<h1>{saludos.spa + ' ' + name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
  <Button updateName={changeName} />
  <Table
    satellites={sats}
    search={handleSearch}
    selectOptions={uniqueCountryOfLaunch}
    selected={filterBy}
  />
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