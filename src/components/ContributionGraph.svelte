<script>
  import Square from "./Square.svelte";

  export let contributions = []
  const colors = ['#ebedf0', '#c6e48b', '#d0f0c0', '#9be58c', '#7bc96f', '#52c41a', '#239a3b', '#3da940', '#196127', '#2a7f29', '#a9d6ac', '#4bb543', '#1f7c1c'];
  function getColor(count) {
    return colors[Math.min(count, colors.length - 1)];
  }

  const currentDate = new Date();
  const currentYear = currentDate.getFullYear();
  const firstDayOfYear = new Date(currentYear, 0, 1);
  const lastDayOfYear = new Date(currentYear, 11, 31);

  let firstMondayOfYear = new Date(firstDayOfYear);
  firstMondayOfYear.setDate(firstMondayOfYear.getDate() + (8 - firstMondayOfYear.getDay()) % 7);

  const graphData = [];
  for (let date = new Date(firstMondayOfYear); date <= lastDayOfYear; date.setDate(date.getDate() + 1)) {
    const year = date.getFullYear();
    const month = date.getMonth() + 1;
    const day = date.getDate();
    const dateString = `${year}-${String(month).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
    const contribution = contributions.find((item) => item.date === dateString);
    graphData.push(contribution || { date: dateString, count: 0 });
  }
</script>
<main>
    <div class="graph">
    <ul class="months">
      <li>Jan</li>
      <li>Feb</li>
      <li>Mar</li>
      <li>Apr</li>
      <li>May</li>
      <li>Jun</li>
      <li>Jul</li>
      <li>Aug</li>
      <li>Sep</li>
      <li>Oct</li>
      <li>Nov</li>
      <li>Dec</li>
    </ul>
    <ul class="days">
      <li>Sun</li>
      <li>Mon</li>
      <li>Tue</li>
      <li>Wed</li>
      <li>Thu</li>
      <li>Fri</li>
      <li>Sat</li>
    </ul>
    <ul class="squares">
      {#each graphData as {date, count}, i}
        <Square
            date={date}
            count={count}
            color={getColor(count)}
        />
      {/each}
    </ul>
  </div>
</main>
<style>
    .months { grid-area: months; }
    .days { grid-area: days; }
    .squares { grid-area: squares; }
    .graph {
        display: inline-grid;
        grid-template-areas: "empty months"
                            "days squares";
        grid-template-columns: auto 1fr;
        grid-gap: 10px;
        padding: 20px;
        border: 1px #e1e4e8 solid;
        margin: 20px;
    }
    .months {
    display: grid;
    grid-template-columns: calc(var(--week-width) * 4) /* Jan */
                            calc(var(--week-width) * 4) /* Feb */
                            calc(var(--week-width) * 4) /* Mar */
                            calc(var(--week-width) * 5) /* Apr */
                            calc(var(--week-width) * 4) /* May */
                            calc(var(--week-width) * 4) /* Jun */
                            calc(var(--week-width) * 5) /* Jul */
                            calc(var(--week-width) * 4) /* Aug */
                            calc(var(--week-width) * 4) /* Sep */
                            calc(var(--week-width) * 5) /* Oct */
                            calc(var(--week-width) * 4) /* Nov */
                            calc(var(--week-width) * 5) /* Dec */;
    }
    .days,
    .squares {
        display: grid;
        grid-gap: var(--square-gap);
        grid-template-rows: repeat(7, var(--square-size));
    }

    .days li{
      line-height: 15px;
    }

    .squares {
        grid-auto-flow: column;
        grid-auto-columns: var(--square-size);
    }

</style>