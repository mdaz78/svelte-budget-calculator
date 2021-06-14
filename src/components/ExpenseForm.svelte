<script>
  import { getContext } from 'svelte';

  import Title from './Title.svelte';

  const { add: addExpense } = getContext('expense');

  const handleSubmit = () => {
    const expense = {
      name,
      amount,
      id: Math.random() * Date.now(),
    };

    name = '';
    amount = null;
    addExpense(expense);
  };

  const title = 'Add Expense';
  let name = '';
  let amount = null;

  $: isEmpty = !name || !amount;
</script>

<section class="form">
  <Title {title} />
  <form class="expense-form" on:submit|preventDefault={handleSubmit}>
    <div class="form-control">
      <label for="name">Name</label>
      <input type="text" id="name" bind:value={name} />
    </div>
    <div class="form-control">
      <label for="amount">Amount</label>
      <input type="number" id="amounr" bind:value={amount} />
    </div>

    {#if isEmpty}
      <p class="form-empty">Pleae Fill Out All Form Fields</p>
    {/if}

    <button
      type="submit"
      class="btn btn-block"
      class:disabled={isEmpty}
      disabled={isEmpty}
    >
      Add Expense
    </button>

    <button type="button" class="close-btn">
      <i class="fas fa-times" />Close
    </button>
  </form>
</section>
