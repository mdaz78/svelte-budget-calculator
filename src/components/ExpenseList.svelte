<script>
  import Title from './Title.svelte';
  import Expense from './Expense.svelte';
  export let expenses = [];

  console.log(expenses);
</script>

<section>
  <Title title="Expense List" />
  <ul>
    {#each expenses as expense}
      <Expense {expense} />
    {:else}
      <h2>Currently you have no expenses</h2>
    {/each}
  </ul>
</section>
