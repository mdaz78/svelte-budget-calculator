<script>
  import { getContext } from 'svelte';
  import { fly } from 'svelte/transition';
  import { flip } from 'svelte/animate';

  import Title from './Title.svelte';
  import Expense from './Expense.svelte';
  export let expenses = [];

  const { clear } = getContext('expense');
</script>

<section>
  <Title title="Expense List" />
  <ul>
    {#each expenses as expense, index (expense.id)}
      <div
        in:fly={{ x: -200, delay: index * 500 }}
        out:fly={{ x: 200 }}
        animate:flip
      >
        <Expense {...expense} />
      </div>
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
