<script>
  import { afterUpdate, onMount } from 'svelte'
  import Table from "./components/Table.svelte"
  import Button from "./components/Button.svelte"
  import Modal from "./components/Modal.svelte"

	export let name;

  const flati = {
    originalUsers: [],
    users: [],
    pronouns: [],
    options: ['first_name', 'last_name', 'username', 'pronouns'],
    searchBy: 'first_name',
    modalShown: false,
  }

  const url = {
    flatilife: 'https://immense-crag-19841.herokuapp.com/users'
  }
  
  const saludos = {
    eng: 'hello',
    spa: 'hola',
    gua: "mba'eichapa"
  }

  const removeDuplicatesFromArray = (array) => {
    let cleanArray = []
    // remove duplicates duplicates values from array   
    if (!array)
      return 

    return cleanArray = [...new Set(array)]
  }

  onMount( () => {
    fetch( url.flatilife )
    .then( data => data.json())
    .then( data => {
      flati.users = [...data]
      flati.originalUsers = [...data]
      flati.originalUsers.forEach( user => flati.pronouns.push( user.pronouns ) )
      flati.pronouns = [...removeDuplicatesFromArray( flati.pronouns )]
    })
  })

  const handleClick = () => {
    name = 'Jose'
    console.log(flati.users)
  }

  const handleSearch = (e) => {
    let search = e.target.value.toLowerCase()
    const result = flati.originalUsers.filter( u => u[flati.searchBy].toLowerCase().includes(search))
    flati.users = [...result]
  }

  const searchBy = (e) => {
    let search = e.target.value
    flati.searchBy = search
  }

  const filterBy = (e) => {
    let filter = e.target.value
    // console.log(filter);
    const result = flati.originalUsers.filter( u => u.pronouns.includes( filter ) )
    flati.users = [...result]
  }

  const handleModal = () => {
    const modal = document.querySelector('.modal')
    if (!flati.modalShown)
      modal.style.display = 'block'
    else
      modal.style.display = 'none'

    flati.modalShown = !flati.modalShown
    // console.log(modal)
  }
</script>

<main>
	<h1>{saludos.spa + ' ' + name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
  <Button handleClick={handleClick} text={'Hola Jose'}/>
  <Button handleClick={handleModal} text={'Open Modal'}/>
  <Table
    dataset={flati}
    search={handleSearch}
    selectOptions={flati.pronouns}
    selected={filterBy}
    options={flati.options}
    searchBy={searchBy}
  />
  <Modal closeModal={handleModal}/>
  <ul>
    {#each flati.users as u}
    <li>User ID: {u.id}</li>
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