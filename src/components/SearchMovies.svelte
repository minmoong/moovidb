<script lang="ts">
  import { goto } from '$app/navigation';
  import { fly } from 'svelte/transition';

  let value = '';
  let active = false;

  function cancelInactive () {
    if (value) {
      active = true;
    } else {
      active = false;
    }
  }

  function submitSearch () {
    goto('/search/' + value);
  }
</script>

<form on:submit|preventDefault={submitSearch} class="search">
  {#if !active}
    <label
      in:fly={{ y: -10, duration: 500 }}
      out:fly={{ y: -10, duration: 500 }}
      for="search_movie">
        영화 검색하기
    </label>
  {/if}
  <input
    on:blur={cancelInactive}
    on:focus={() => active = true}
    bind:value
    name="search_movie"
    type="text"
    class:selected={active}
    autocomplete="off"
  />
  {#if value}
    <button
      in:fly={{ x: 20, duration: 500 }}
      out:fly={{ x: 0, duration: 500 }}>
        검색
    </button>
  {/if}
</form>

<style>
  .search {
    position: relative;
    width: 40%;
    margin: 0 auto 40px;
    filter: drop-shadow(2px 4px 6px rgba(0, 0, 0, 0.2));
  }

  @media (max-width: 720px) {
    .search {
      width: 90%;
    }
  }

  button {
    font-size: 1rem;
    padding: 0rem 1rem;
    background: #fff;
    color: rgb(63, 63, 63);
    font-weight: bold;
    border: none;
    position: absolute;
    bottom: 50%;
    right: 0;
    transform: translate(0, 50%);
    height: 100%;
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
    cursor: pointer;
  }

  input {
    width: 100%;
    border: none;
    font-size: 1.2rem;
    outline: none;
    color: #fff;
    padding: 0.5rem 0.1rem;
    transition: background 0.75s ease-out;
    background: rgb(255, 255, 255);
    border-radius: 10px;
    padding: 1rem;
  }

  label {
    position: absolute;
    font-size: 1.2rem;
    top: 50%;
    left: 0;
    transform: translate(0, -50%);
    pointer-events: none;
    color: #000;
    padding: 0rem 1rem;
  }

  input.selected {
    background:rgb(63, 63, 63);
  }
</style>
