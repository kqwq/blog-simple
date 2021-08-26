<script>
  import Nav from "$lib/Nav.svelte";
</script>


<dir class="container">
  <Nav />
  <slot />
</dir>

<style>
  .container {
    max-width: 800px;
    margin: 50px auto;
  }

</style>