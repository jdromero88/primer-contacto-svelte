<script>
  import tippy from "sveltejs-tippy"

  export let handleClick
  export let text = 'Click Me'

  // Handle tippy
  const tippyProps = {
    content: text,
    placement: "bottom"
  }
</script>

<button use:tippy={tippyProps} on:click={handleClick}>
  {text}!
</button>

<style>

</style>