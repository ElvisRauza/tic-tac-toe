<script>
  import Game from "./lib/Game.svelte";
</script>

<main>
  <h1>Tic tac Toe!</h1>

  <Game />
</main>

<style>
  :global(*) {
    box-sizing: border-box;
  }

  :global(body) {
    font-family: "Montserrat", sans-serif;
  }

  :root {
    --player-1: #0017e7;
    --player-2: #ff7b00;
  }

  h1 {
    font-size: 3rem;
    text-align: center;
  }
</style>
