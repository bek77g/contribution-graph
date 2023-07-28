<script>
  import ContributionGraph from "./components/ContributionGraph.svelte";
  const contributions = [
    { date: '2023-06-30', count: 3 },
    { date: '2023-07-01', count: 5 },
    { date: '2023-07-02', count: 10 },
    { date: '2023-07-03', count: 10 },
    { date: '2023-07-04', count: 5 },
    { date: '2023-07-05', count: 6 },
    { date: '2023-07-06', count: 7 },
    { date: '2023-02-06', count: 7 },
  ];
</script>

<main>
  <ContributionGraph contributions={contributions}/>
</main>