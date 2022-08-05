<script>
  import Ripple from '@smui/ripple';
</script>

<nav>
  <a href="/" use:Ripple={{ surface: true }}>Movie Database</a>
</nav>

<style>
  nav {
    display: flex;
    min-height: 10vh;
    align-items: center;
    justify-content: center;
  }

  a {
    font-size: 2rem;
    font-weight: bold;
    text-decoration: none;
    padding: 20px;
    border-radius: 13px;
  }
</style>