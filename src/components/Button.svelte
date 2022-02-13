<script>
  export let handleClick
  export let text = 'Click Me'
</script>

<button on:click={handleClick}>
  {text}!
</button>

<style>

</style>