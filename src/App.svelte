<script>
  import Nav from './components/Nav.svelte';
  import expensesData from './expenses';
  import ExpenseList from './components/ExpenseList.svelte';

  let expenses = [...expensesData];
</script>

<Nav />

<main class="content">
  <ExpenseList {expenses} />
</main>
