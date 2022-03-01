<script>
  import { afterUpdate, onMount } from 'svelte'

  import Router from 'svelte-spa-router'

  import Home from './pages/Home.svelte'
  import About from './pages/About.svelte'
  import Products from './pages/Products.svelte'
  import NotFound from './pages/NotFound.svelte'

  import Navigation from './components/Navigation.svelte'
  import Table from "./components/Table.svelte"
  import Button from "./components/Button.svelte"
  import Modal from "./components/Modal.svelte"

	export let name;

  const routes = {
  "/": Home,
  "/about": About,
  "/products": Products,

  "*": NotFound
}

  const flati = {
    originalUsers: [],
    users: [],
    pronouns: [],
    options: ['first_name', 'last_name', 'username', 'pronouns'],
    searchBy: 'first_name',
    modalShown: false,
  }

  const url = {
    googleAPIKey: 'AIzaSyBXuQRRw4K4W8E4eGHoSFUSrK-ZwpD4Zz4',
    googleSpreadsheetKey: "1a09uVgZMOQli01YIS7TGvDcKZurys6_eK03ZBY7J5HQ",
    googleSpreadsheetRange: "Sheet1",
    googleS: "https://docs.google.com/spreadsheets/d/1CMSgbRGJqSJfwsSftprzC3e-pL6FC2eDEc4xE3BFQwc/edit#gid=0",
    flatilife: 'https://immense-crag-19841.herokuapp.com/users'
  }

  // `https://sheets.googleapis.com/v4/spreadsheets/1CMSgbRGJqSJfwsSftprzC3e-pL6FC2eDEc4xE3BFQwc/`

  // `https://sheets.googleapis.com/v4/spreadsheets/${googleSpreadsheetKey}?key=${googleAPIKey}`

  // `https://sheets.googleapis.com/v4/spreadsheets/1CMSgbRGJqSJfwsSftprzC3e-pL6FC2eDEc4xE3BFQwc/`

  // `https://sheets.googleapis.com/v4/spreadsheets/1a09uVgZMOQli01YIS7TGvDcKZurys6_eK03ZBY7J5HQ?key=AIzaSyBXuQRRw4K4W8E4eGHoSFUSrK-ZwpD4Zz4`

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

    fetch( `https://sheets.googleapis.com/v4/spreadsheets/${url.googleSpreadsheetKey}/values/${url.googleSpreadsheetRange}?key=${url.googleAPIKey}`)
    .then( data => data.json())
    .then(data => console.log(data))
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
  <Navigation />
  <Router {routes} />
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
  <Modal closeModal={handleModal} tippyText={'Close Modal'} />
  <ul>
    {#each flati.users as u}
    <li>User ID: {u.id}</li>
    {/each}
  </ul>
</main>

<style lang='scss' global>
  @use './scss/main.scss';
</style>