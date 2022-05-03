<script>
  import { onMount } from 'svelte';
  import Info from './Info.svelte';
  let characters = [];
  let errorMessage;

  const getChars = async () => {
    const response = await fetch(`https://swapi.dev/api/people/`);
    if (!response.ok) {
      throw new Error('An error has occurred');
    }
    return await response.json();
  };
  onMount(() =>
    getChars()
      .then((data) => {
        characters = data.results;
      })
      .catch((err) => {
        errorMessage = err.message;
      })
  );
  let charInfo;
  let infoVisible = false;

  const infoVisibility = (ind) => {
    infoVisible = true;
    charInfo = ind;
  };
</script>

<main>
  <h1>Star Wars</h1>
  {#each characters as character, i}
    <div class="chars" on:click={() => infoVisibility(i)}>
      {character.name}
    </div>
  {:else}
    {#if errorMessage}
      <div>{errorMessage}</div>
    {:else}
      <div>Loading...</div>
    {/if}
  {/each}
</main>
{#if infoVisible}
  <Info
    name={characters[charInfo].name}
    gender={characters[charInfo].gender}
    birth_year={characters[charInfo].birth_year}
    height={characters[charInfo].height}
    mass={characters[charInfo].mass}
    on:hide={() => (infoVisible = false)}
  />
{/if}

<style>
  .chars {
    margin: 1em;
    font-size: 1em;
  }
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 3em;
    font-weight: 100;
    padding-top: 1em;
  }
  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
