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
  }
</style>

<h3>Добавить новый вклад</h3>
<form on:submit|preventDefault>
  <label>
    Дата:
    <input type="date" bind:value={newDate} />
  </label>
  <label>
    Количество:
    <input type="number" bind:value={newCount} />
  </label>
  <button on:click={() => addContribution(newDate, +newCount)}>Добавить</button>
</form>

<h3>Текущие вклады</h3>
<table class="contributions-table">
  <thead>
    <tr>
      <th>Дата</th>
      <th>Количество</th>
      <th>Действия</th>
    </tr>
  </thead>
  <tbody>
    {#each contributions as { date, count }, i}
      <tr>
        <td>{date}</td>
        <td>{count}</td>
        <td>
          <button on:click={() => dispatch('update', { index: i, count: +prompt('Введите новое количество:', count) })}>Изменить</button>
          <button on:click={() => deleteContribution(i)}>Удалить</button>
        </td>
      </tr>
    {/each}
  </tbody>
</table>

<ContributionGraph contributions={contributions} />

