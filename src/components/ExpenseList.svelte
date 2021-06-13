<script>
  import { getContext } from 'svelte';

  import Title from './Title.svelte';
  import Expense from './Expense.svelte';
  export let expenses = [];

  const { clear } = getContext('expense');
</script>

<section>
  <Title title="Expense List" />
  <ul>
    {#each expenses as expense}
      <Expense {...expense} />
    {:else}
      <h2>No expense added to the list!</h2>
    {/each}
  </ul>

  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={() => clear()}
  >
    Clear Expenses
  </button>
</section>

<style>
  h2 {
    text-transform: capitalize;
  }
</style>
