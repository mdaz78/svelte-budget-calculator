<script>
  export let expense = {};
  let { name, amount } = expense;
  let displayAmount = false;

  function toggleDisplayAmount() {
    console.log('clicked');
    displayAmount = !displayAmount;
  }
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2 on:click={() => toggleDisplayAmount()} class="cursor-pointer">
      {name}
      <button class="amount-btn"><i class="fas fa-caret-down" /></button>
    </h2>

    {#if displayAmount}
      <h4>amount: ${amount}</h4>
    {/if}
  </div>

  <div class="expense-buttons">
    <button class="expense-btn edit-btn"> <i class="fas fa-pen" /> </button>

    <button class="expense-btn delete-btn"> <i class="fas fa-trash" /> </button>
  </div>
</article>

<style>
  .cursor-pointer {
    cursor: pointer;
  }
</style>
