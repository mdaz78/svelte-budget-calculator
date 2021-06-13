<script>
  import { setContext } from 'svelte';

  import Nav from './components/Nav.svelte';
  import expensesData from './expenses';
  import ExpenseList from './components/ExpenseList.svelte';

  let expenses = [...expensesData];

  const removeExpense = (id) => {
    expenses = expenses.filter((expense) => expense.id !== id);
  };

  const clearExpenses = () => (expenses = []);

  const expense = {
    remove: removeExpense,
    clear: clearExpenses,
  };

  setContext('expense', expense);
</script>

<Nav />

<main class="content">
  <ExpenseList {expenses} {removeExpense} />
</main>
