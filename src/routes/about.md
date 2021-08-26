# About

lorem ipsum

<script>
  import Box from "./Box.svelte"
  let count = 10
</script>

{count}

<button on:click={() => count ++}>Increment {count}</button>

<Box />
