<script>
  import { setContext } from 'svelte';

  import Nav from './components/Nav.svelte';
  import Title from './components/Title.svelte';
  import expensesData from './expenses';
  import ExpenseList from './components/ExpenseList.svelte';
  import ExpenseForm from './components/ExpenseForm.svelte';

  let expenses = [...expensesData];

  $: isEditing = setId ? true : false;
  $: total = expenses.reduce((sum, { amount }) => (sum += amount), 0);

  let setName = '';
  let setAmount = null;
  let setId = null;

  let isFormOpen = false;

  const showForm = () => (isFormOpen = true);
  const hideForm = () => {
    isFormOpen = false;
    setName = '';
    setAmount = null;
    setId = null;
  };

  const removeExpense = (id) => {
    expenses = expenses.filter((expense) => expense.id !== id);
  };

  const clearExpenses = () => (expenses = []);

  const addExpense = (expense) => {
    expenses = [expense, ...expenses];
  };

  const updateExpense = (id) => {
    let expense = expenses.find((item) => item.id === id);

    setName = expense.name;
    setAmount = expense.amount;
    setId = expense.id;
    showForm();
  };

  const editExpense = ({ name, amount }) => {
    expenses = expenses.map((expense) => {
      if (expense.id === setId) {
        return { ...expense, name, amount };
      } else {
        return { ...expense };
      }
    });

    hideForm();
  };

  const expense = {
    remove: removeExpense,
    clear: clearExpenses,
    add: addExpense,
    update: updateExpense,
    edit: editExpense,
  };

  setContext('expense', expense);
</script>

<Nav {showForm} />
<main class="content">
  {#if isFormOpen}
    <ExpenseForm name={setName} amount={setAmount} {isEditing} {hideForm} />
  {/if}
  <Title title={`Total Expenses : $${total}`} />
  <ExpenseList {expenses} {removeExpense} />
</main>
