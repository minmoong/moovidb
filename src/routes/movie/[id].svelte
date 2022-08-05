<script context="module" lang="ts">
  import type { Load } from '@sveltejs/kit';

  export const load: Load = async ({ fetch, params }) => {
    const res = await fetch(
      `https://api.themoviedb.org/3/movie/${params.id}?api_key=${
        import.meta.env.VITE_API
      }&language=ko`
    );
    const movieDetail = await res.json();
    if (res.ok) {
      return {
        props: { movieDetail }
      };
    }

    const { message } = await res.json();
    return {
      error: new Error(message)
    };
  }
</script>

<script lang="ts">
  import { fly } from 'svelte/transition';
  export let movieDetail: MovieDetail;
</script>

<div class="movie-details"  in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
  <div class="img-container">
    <img
      src={'https://image.tmdb.org/t/p/original' + movieDetail.backdrop_path}
      alt={movieDetail.title}
    />
  </div>
  <div class="txt-container">
    <h1>{movieDetail.title}</h1>
    <p class="overview">{movieDetail.overview}</p>
    <p>
      <span>출시일:</span> {movieDetail.release_date} <br />
      <span>예산:</span> {movieDetail.budget}원 <br />
      <span>평점:</span> {movieDetail.vote_average}점 <br />
      <span>상영 시간:</span> {movieDetail.runtime}분
    </p>
  </div>
</div>

<style>
  h1 {
    padding: 1rem 0rem 2rem;
  }

  p {
    padding: 1rem 0rem;
  }

  .img-container {
    width: 100%;
  }

  img {
    width: 100%;
    border-radius: 1rem;
  }

  .movie-details {
    margin: 2rem 20%;
  }

  span {
    font-weight: bold;
  }
</style>