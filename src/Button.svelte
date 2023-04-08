<script>
  export let type = 'button';
</script>

<button on:click {type}><slot /></button>

<style>
  button {
    padding: 10px 20px;
    border-radius: 20px;
    font-size: 18px;
    margin: auto;
    cursor: pointer;
    background-color: #7db9e8;
    color: #3b5998;
  }
  button:hover {
    box-shadow: 0 12px 16px 0 rgba(0, 0, 0, 0.24),
      0 17px 50px 0 rgba(0, 0, 0, 0.19);
    transition-duration: 0.4s;
  }

  button:disabled {
    background-color: #ccc;
  }
</style>
