<script>
  export let checkType;
</script>

<div
  class="cell {checkType ? `cell--${checkType}` : null}"
  class:cell--disabled={checkType}
  on:click
>
  {#if 1 === checkType}
    <span>X</span>
  {:else if 2 === checkType}
    <span>O</span>
  {/if}
</div>

<style lang="scss">
  .cell {
    cursor: pointer;

    width: 100px;
    height: 100px;
    border: 1px solid black;

    font-size: 4rem;
    font-weight: 700;
    text-align: center;
    line-height: 100px;

    &--1 {
      color: var(--player-1);
    }
    &--2 {
      color: var(--player-2);
    }

    &--disabled {
      cursor: default;
      pointer-events: none;
    }
  }
</style>
