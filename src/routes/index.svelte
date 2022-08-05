<script context="module" lang="ts">
  import type { Load } from '@sveltejs/kit';

  export const load: Load = async ({ fetch }) => {
    const res = await fetch(
      `https://api.themoviedb.org/3/movie/popular?api_key=${
        import.meta.env.VITE_API
      }&language=ko&page=1`
    );
    const data = await res.json();
    if (res.ok) {
      return {
        props: { popular: data.results }
      };
    }

    const { message } = await res.json();
    return {
      error: new Error(message)
    };
  }
</script>

<script lang="ts">
  import PopularMovies from 'src/components/PopularMovies.svelte';
  import SearchMovies from 'src/components/SearchMovies.svelte';
  import { fly } from 'svelte/transition';
  export let popular: Movie[];
</script>

<section in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
  <SearchMovies />
  <PopularMovies {popular} />
</section>