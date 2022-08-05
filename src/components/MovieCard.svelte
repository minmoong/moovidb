<script lang="ts">
  import Ripple from '@smui/ripple';
  export let movie: Movie;
</script>

<div class="movie-card">
  <div use:Ripple={{ surface: true }}>
    <a sveltekit:prefetch sveltekit:noscroll href={'/movie/' + movie.id}>
      <img src={'https://image.tmdb.org/t/p/w500' + movie.poster_path} alt={movie.title} />
    </a>
    <div class="description">
      <h2>{movie.title}</h2>
      <p>{movie.release_date}</p>
    </div>
  </div>
</div>

<style>
  img {
    width: 100%;
    height: 30vh;
    object-fit: cover;
    border-radius: 1rem;
    margin-bottom: 1rem;
    filter: drop-shadow(2px 4px 6px rgba(0, 0, 0, 0.2));
  }

  h2 {
    font-size: 1.3rem;
  }

  .description {
    height: 5vh;
  }

  p {
    font-size: 1rem;
  }

  .movie-card {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
  }

  .movie-card > div {
    padding: 1rem 1rem 2rem;
  }
</style>