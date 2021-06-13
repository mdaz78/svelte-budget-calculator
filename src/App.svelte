<script>
  import { setContext } from 'svelte';

  import Nav from './components/Nav.svelte';
  import expensesData from './expenses';
  import ExpenseList from './components/ExpenseList.svelte';

  let expenses = [...expensesData];

  const removeExpense = (id) => {
    expenses = expenses.filter((expense) => expense.id !== id);
  };

  const expense = {
    remove: removeExpense,
  };

  setContext('expense', expense);
</script>

<Nav />

<main class="content">
  <ExpenseList {expenses} {removeExpense} />
</main>
