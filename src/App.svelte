<script>
  import { setContext } from 'svelte';

  import Nav from './components/Nav.svelte';
  import Title from './components/Title.svelte';
  import expensesData from './expenses';
  import ExpenseList from './components/ExpenseList.svelte';
  import ExpenseForm from './components/ExpenseForm.svelte';

  let expenses = [...expensesData];

  $: total = expenses.reduce((sum, { amount }) => (sum += amount), 0);

  const removeExpense = (id) => {
    expenses = expenses.filter((expense) => expense.id !== id);
  };

  const clearExpenses = () => (expenses = []);

  const addExpense = (expense) => {
    expenses = [expense, ...expenses];
  };

  const expense = {
    remove: removeExpense,
    clear: clearExpenses,
    add: addExpense,
  };

  setContext('expense', expense);
</script>

<Nav />

<main class="content">
  <ExpenseForm />
  <Title title={`Total Expenses : $${total}`} />
  <ExpenseList {expenses} {removeExpense} />
</main>
