<script>
  import Board from "./Board.svelte";

  const Players = {
    1: "X",
    2: "O",
  };

  let gameState = null;
  let isGameRunning = true;

  let currentPlayer = 1;

  let board = [null, null, null, null, null, null, null, null, null];

  function checkBoard() {
    const emptyCells = board.filter((item) => !item);

    if (checkIfWon()) {
      // Check if won
      isGameRunning = false;
      gameState = currentPlayer;
    } else if (0 === emptyCells.length) {
      // If all cells filled
      isGameRunning = false;
      gameState = "draw";
    } else {
      // Switch player
      currentPlayer = 1 === currentPlayer ? 2 : 1;
    }
  }

  function checkIfWon() {
    let playerWon = false;

    // Horizontal checks.
    for (let i = 0; i < 3; i++) {
      // 0 == 1 == 2
      // 3 == 4 == 5
      // 6 == 7 == 8
      if (
        currentPlayer === board[i * 3] &&
        currentPlayer === board[i * 3 + 1] &&
        currentPlayer === board[i * 3 + 2]
      ) {
        playerWon = true;
      }
    }
    // Vertical checks.
    for (let i = 0; i < 3; i++) {
      // 0 == 3 == 6
      // 1 == 4 == 7
      // 2 == 5 == 8
      if (
        currentPlayer === board[i] &&
        currentPlayer === board[i + 3] &&
        currentPlayer === board[i + 6]
      ) {
        playerWon = true;
      }
    }
    // Diagonal checks
    if (
      currentPlayer === board[2] &&
      currentPlayer === board[4] &&
      currentPlayer === board[6]
    ) {
      playerWon = true;
    }
    if (
      currentPlayer === board[0] &&
      currentPlayer === board[4] &&
      currentPlayer === board[8]
    ) {
      playerWon = true;
    }

    return playerWon;
  }

  function resetGame() {
    for (let i = 0; i < 9; i++) {
      board[i] = "";
      board = board;
    }

    gameState = null;
    isGameRunning = true;
  }

  function handleUserChangedCell(event) {
    board[event.detail.index] = event.detail.player;
    board = board;
    // Check if won
    checkBoard();
  }
</script>

<div class="tic-tac-toe">
  {#if isGameRunning}
    <p class="tic-tac-toe__heading">
      It's Player
      <span class="tic-tac-toe__player tic-tac-toe__player--{currentPlayer}"
        >{Players[currentPlayer]}</span
      >
      turn!
    </p>
  {:else}
    <p class="tic-tac-toe__heading">&nbsp;</p>
  {/if}
  <Board
    {board}
    {isGameRunning}
    {currentPlayer}
    on:userChangedCell={handleUserChangedCell}
  />
  {#if !isGameRunning}
    <div class="tic-tac-toe__message">
      {#if "draw" === gameState}
        <p>Game is Draw!</p>
      {:else if gameState}
        <p>
          Player <span
            class="tic-tac-toe__player tic-tac-toe__player--{currentPlayer}"
            >{Players[currentPlayer]}</span
          > won the game!
        </p>
      {/if}
      <button class="btn" on:click={resetGame}>Restart!</button>
    </div>
  {/if}
</div>

<style lang="scss">
  .btn {
    cursor: pointer;
    border: none;
    border-radius: 0;

    font-size: 1.25rem;
    line-height: 1;
    padding: 10px 20px;
    color: white;
    background-color: black;
  }

  .tic-tac-toe {
    text-align: center;

    &__heading {
      font-size: 1.75rem;
    }

    &__player {
      font-weight: 700;

      &--1 {
        color: var(--player-1);
      }

      &--2 {
        color: var(--player-2);
      }
    }

    &__message {
      font-size: 1.75rem;
    }
  }
</style>
