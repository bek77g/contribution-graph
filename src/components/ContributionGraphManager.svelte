<script>
  import { createEventDispatcher } from 'svelte';
  import ContributionGraph from './ContributionGraph.svelte';

  export let contributions = [];

  let newDate = '';
  let newCount = '';

  function addContribution(date, count) {
    contributions = [...contributions, { date, count }];
  }
  function updateContribution(index, count) {
    contributions = contributions.map((contribution, i) =>
      i === index ? { ...contribution, count } : contribution
    );
  }

  function deleteContribution(index) {
    contributions = contributions.filter((_, i) => i !== index);
  }

  const dispatch = createEventDispatcher();
</script>

<style>
  .contributions-table{
    margin: 0 auto;
    max-width: 500px;
  }
  .contributions-table thead,
  .contributions-table tbody tr{
    display: table;
    table-layout: fixed;
    width: 100%;
  }
  .contributions-table tbody{
    display: block;
    max-height: 30vh;
    overflow-y: scroll;
    width: 100%;
  }
</style>

<h3>Add a new contribution</h3>
<form on:submit|preventDefault>
  <label>
    Date:
    <input type="date" bind:value={newDate} />
  </label>
  <label>
    Count:
    <input type="number" bind:value={newCount} />
  </label>
  <button on:click={() => addContribution(newDate, +newCount)}>Add</button>
</form>

<h3>Current contributions</h3>
<table class="contributions-table">
  <thead>
    <tr>
      <th>Date</th>
      <th>Count</th>
      <th>Actions</th>
    </tr>
  </thead>
  <tbody>
    {#each contributions as { date, count }, i}
      <tr>
        <td>{date}</td>
        <td>{count}</td>
        <td>
          <button on:click={() => updateContribution(i, +prompt('Введите новое количество:', count))}>Edit</button>
          <button on:click={() => deleteContribution(i)}>Delete</button>
        </td>
      </tr>
    {/each}
  </tbody>
</table>

<ContributionGraph contributions={contributions} />

