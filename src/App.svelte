<script>
  import Footer from './Footer.svelte';
  import Todos from './Todos.svelte';
  export let name;
  let todos = ['Siivoa huone', 'Pese hampaat'];

  /*
  Luodaan poista funktion, jotta voidaan poistaa todoja todos taulukosta.
  Funktio saa event parametrin, joka sisältää event.detail ominaisuuden, jonka 
  arvo saadaan poista tapahtuman yhteydessä. 
  */

  function poista(event) {
    todos = todos.filter((t) => t !== event.detail);
  }

  /*
  Luodaan lisaaTodo funktio ja alustetaan uusitodo muuttuja. Funktio saa event parametrin, joka sisältää event.detail ominaisuuden, jonka 
  arvo saadaan lisaa tapahtuman yhteydessä. 
  */

  function lisaa(event) {
    let uusitodo = event.detail;
    todos = [...todos, uusitodo];
  }
</script>

<main>
  <h1>{name}n ToDo app</h1>
  <!--Todos komponentti käyttöön, on:poista tapahtuma joka laukaisee luodun poista fuktion -> todo poistuu. on:lisaa tapahtuma, joka laukaisee lisaaTodo
  funktion -> uusi todo lisätään  -->
  <Todos {todos} on:poista={poista} on:lisaa={lisaa} />
  <!--Footer componentti käyttöön, jolle välitetään name muuttuja-->
  <Footer text="TodoApp by" {name} />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 800px;
    margin: 0 auto;
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  }

  h1 {
    color: #4a4a4a;
    text-transform: uppercase;
    font-size: 3.5em;
    font-weight: 700;
    margin-top: 0, 5em;
    margin-bottom: 0, 5em;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
