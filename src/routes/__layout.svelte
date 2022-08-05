<script>
  import '../app.css';
  import Nav from 'src/components/Nav.svelte';
</script>

<main>
  <Nav />
  <slot />
</main>

<style>
  main {
    height: 100vh;
    background-color: #21D4FD;
    background-image: linear-gradient(19deg, #21D4FD 0%, #B721FF 100%);
    overflow: auto;
  }
</style>