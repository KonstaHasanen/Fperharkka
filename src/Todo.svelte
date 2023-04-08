<script>
  //Tuodaan crateEventDispatcher funktio svelten kirjastosta
  import { createEventDispatcher } from 'svelte';
  import Button from './Button.svelte';
  export let todo;
  let tehty = false;

  //Otetaan crateEventDispatcher funktio käyttöön
  const dispatch = createEventDispatcher();

  /*
    Luodaan poistaTodo funktio, joka käyttää dispatch metodia Metodi saa parametrinaan tapahtuman nimen 'poista' sekä poistettavan asian eli todo muuttujan. 
  */
  const poistaTodo = () => {
    dispatch('poista', todo);
  };

  /*
  Luodaan merkitseTehdyksi funktio, jonka tarkoituksena on muuttaa muuttujan tehty arvo falsesta trueksi. Arvon muuttuessa astuu voimaan alla olevat css säännöt.
  */
  const merkitseTehdyksi = () => {
    tehty = !tehty;
  };
</script>

<main>
  <!--jos tehty muuttuja on true käytetään .todo.tehty css määrityksiä
      muussa tapauksessa käytetään ainoastaan .todo css määrityksiä -->
  <div class="todo {tehty ? 'tehty' : ''}">
    <p>{todo}</p>
    <div>
      <!--Button komponentti käyttöön, jos käyttäjä klikkaa buttonia suoritetaan poistaTodo funktio-->
      <Button on:click={poistaTodo}>
        <i class="fa fa-trash" />
      </Button>

      <!--Button komponentti käyttöön, jos käyttäjä klikkaa buttonia suoritetaan merkitseTehdyksi funktio-->
      <Button on:click={merkitseTehdyksi}>
        <i class="fa fa-check" />
      </Button>
    </div>
  </div>
</main>

<style>
  .todo {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    border: 1px solid white;
    background: linear-gradient(45deg, #3b5998, #6699cc);
    color: #ffffff;
    font-size: 20px;
    font-family: Georgia, 'Times New Roman', Times, serif;
    margin-left: 20em;
    margin-right: 20em;
    margin-bottom: 1em;
    border-radius: 20px;
  }
  .todo:hover {
    box-shadow: 0 12px 16px 0 rgba(0, 0, 0, 0.24),
      0 17px 50px 0 rgba(0, 0, 0, 0.19);
    transition-duration: 0.4s;
  }

  .todo.tehty {
    text-decoration: line-through;
    opacity: 0.5;
  }
</style>
