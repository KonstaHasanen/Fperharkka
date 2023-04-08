<script>
  import Button from './Button.svelte';
  //Tuodaan crateEventDispatcher funktio svelten kirjastosta
  import { createEventDispatcher } from 'svelte';
  //Otetaan käyttöön svelten fade transition, jotta saadaan sivulle elävyyttä
  import { fade } from 'svelte/transition';

  //Otetaan crateEventDispatcher funktio käyttöön
  const dispatch = createEventDispatcher();

  let uusitodo = '';
  let virheviesti = '';

  /*
  Luodaan lisaaTodo funktio, jossa ensimmäisenä on virheen tarkastus eli toisin sanoen ei voi lisätä tyhjää todoa vaan tulee virheviesti. Lisäksi funktiossa on dispatch metodi, jolla on parametreina lisaa sekä uusitodo muuttuja. 
  */

  function lisaaTodo() {
    if (uusitodo.trim() === '') {
      virheviesti = 'Tehtävä ei voi olla tyhjä!';
    } else {
      dispatch('lisaa', uusitodo);
      uusitodo = '';
    }
  }

  /*
  Luodaan tyhjennaInput funktio, jonka avulla saadaan virheviesti pois
  näkyvistä mikäli input elementti ei ole tyhjä.
  */
  function tyhjennaInput() {
    virheviesti = '';
  }
</script>

<!--on:submit tapahtuma, suoritetaan lisaaTodo funktio enteriä painettaessa-->
<form on:submit|preventDefault={lisaaTodo}>
  <input
    type="text"
    placeholder="Lisää uusi Tehtävä"
    bind:value={uusitodo}
    on:input={tyhjennaInput}
  />
  <!--Button komponentti käyttöön, jos käyttäjä klikkaa buttonia suoritetaan lisaaTodo funktio-->
  <Button on:click={lisaaTodo}>
    <i class="fa fa-plus" />
  </Button>
</form>

{#if virheviesti}
  <!--Otetaan fade transition käyttöön-->
  <div transition:fade>
    <p class="virhe">{virheviesti}</p>
  </div>
{/if}

<style>
  input {
    border: 1px solid #ccc;
    padding: 1em;
    margin-bottom: 0, 5em;
    background-color: #fff;
    border-radius: 20px;
    height: 40px;
    width: 350px;
  }

  .virhe {
    color: red;
    align-items: center;
    text-transform: uppercase;
  }
</style>
