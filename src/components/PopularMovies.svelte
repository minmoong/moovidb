<script lang="ts">
  import MovieCard from './MovieCard.svelte';
  export let popular: Movie[];
</script>

<h3>무비디비 - 인기 영화</h3>
<div class="popular-movies">
  {#each popular as movie}
    <MovieCard {movie} />
  {/each}
</div>

<style>
  h3 {
    padding: 0 1rem;
    font-size: calc(1em + 1vw);
  }

  .popular-movies {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    grid-column-gap: 1rem;
    grid-row-gap: 2rem;
  }
</style>