<script>
  import { getContext } from 'svelte';

  import Title from './Title.svelte';

  const { add: addExpense, edit: editExpense } = getContext('expense');

  export let name = '';
  export let amount = null;
  export let isEditing = false;
  export let hideForm;

  const handleSubmit = () => {
    if (isEditing) {
      editExpense({ name, amount });
    } else {
      const expense = {
        name,
        amount,
        id: Math.random() * Date.now(),
      };
      addExpense(expense);
    }

    name = '';
    amount = null;
  };

  const title = 'Add Expense';

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
      {#if isEditing}
        Edit Expense
      {:else}
        Add Expense
      {/if}
    </button>

    <button type="button" class="close-btn" on:click={hideForm}>
      <i class="fas fa-times" />Close
    </button>
  </form>
</section>
