<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  setTimeout(() => {
    dispatch('hide');
  }, 3000);

  export let name;
  export let height;
  export let mass;
  export let birth_year;
  export let gender;
</script>

<div class="infoBox">
  <p><b>Name: </b> {name}</p>
  <p><b>Gender: </b> {gender}</p>
  <p><b>Year of birth: </b> {birth_year}</p>
  <p><b>Height: </b> {height} cm</p>
  <p><b>Mass: </b> {mass} kg</p>
</div>

<style>
  .infoBox {
    background-color: #ccc;
    border: 1px solid black;
    padding: 1em;
    text-align: center;
    position: fixed;
    top: 2em;
    right: 2em;
    width: 20em;
  }
</style>
