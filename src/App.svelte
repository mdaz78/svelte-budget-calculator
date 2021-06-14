<script>
  import { afterUpdate, onMount, setContext } from 'svelte';

  import Nav from './components/Nav.svelte';
  import Title from './components/Title.svelte';
  import ExpenseList from './components/ExpenseList.svelte';
  import ExpenseForm from './components/ExpenseForm.svelte';
  import Modal from './components/Modal.svelte';

  // import expensesData from './expenses';

  let expenses = [];

  $: isEditing = setId ? true : false;
  $: total = expenses.reduce((sum, { amount }) => (sum += amount), 0);

  let setName = '';
  let setAmount = null;
  let setId = null;

  let isFormOpen = false;

  // forms
  const showForm = () => (isFormOpen = true);
  const hideForm = () => {
    isFormOpen = false;
    setName = '';
    setAmount = null;
    setId = null;
  };

  // expense CRUD
  const removeExpense = (id) => {
    expenses = expenses.filter((expense) => expense.id !== id);
  };

  const clearExpenses = () => {
    expenses = [];
  };

  const addExpense = (expense) => {
    expenses = [expense, ...expenses];
    hideForm();
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

  // local Storage
  const setLocalStorage = (expenses) => {
    localStorage.setItem('expenses', JSON.stringify(expenses));
  };

  const getExpensesFromLocalStorage = () => {
    let expenses = localStorage.getItem('expenses');

    if (expenses) {
      return JSON.parse(expenses);
    } else {
      return null;
    }
  };

  // lifecycle method
  onMount(() => {
    expenses = getExpensesFromLocalStorage() || [];
  });

  afterUpdate(() => {
    setLocalStorage(expenses);
  });
</script>

<Nav {showForm} />
<main class="content">
  {#if isFormOpen}
    <Modal>
      <ExpenseForm name={setName} amount={setAmount} {isEditing} {hideForm} />
    </Modal>
  {/if}
  <Title title={`Total Expenses : $${total}`} />
  <ExpenseList {expenses} {removeExpense} />
</main>
