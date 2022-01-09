<script>
  import { createEventDispatcher } from "svelte";
  import Cell from "./Cell.svelte";

  const dispatch = createEventDispatcher();

  export let isGameRunning;
  export let currentPlayer;
  export let board;

  function handleClick(i) {
    // Check game state
    if (!isGameRunning) {
      return;
    }

    // Check if cell empty
    if (board[i]) {
      return;
    }

    dispatch("userChangedCell", {
      index: i,
      player: currentPlayer,
    });
  }
</script>

<div class="board">
  {#each board as item, i}
    <Cell
      checkType={item}
      on:click={() => {
        handleClick(i);
      }}
    />
  {/each}
</div>

<style>
  .board {
    display: flex;
    flex-wrap: wrap;

    width: 300px;
    margin: 0 auto;
  }
</style>
