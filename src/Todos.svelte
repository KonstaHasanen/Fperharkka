<script>
  import Todo from './Todo.svelte';
  import Uusitodo from './Uusitodo.svelte';
  //Otetaan käyttöön svelten fly transition, jotta saadaan sivulle elävyyttä
  import { fly } from 'svelte/transition';
  export let todos;
</script>

<main>
  <Uusitodo on:lisaa />
  {#each todos as todo}
    <!--Käytetään fly transitioita-->
    <div transition:fly|local={{ x: 15, y: 15 }}>
      <!--Todo komponentti käyttöön, poista tapahtuma käyttöön-->
      <Todo {todo} on:poista />
    </div>
  {/each}
  {#if todos.length === 0}
    <p>Kaikki tehtävät suoritettu!</p>
  {/if}
</main>

<style>
  p {
    font-size: 20px;
    font-family: Georgia, 'Times New Roman', Times, serif;
    padding: 4em;
    background-image: linear-gradient(to bottom, #7db9e8, #3b5998);
    color: #333;
    margin-left: 20em;
    margin-right: 20em;
    border-radius: 20em;
  }
</style>
