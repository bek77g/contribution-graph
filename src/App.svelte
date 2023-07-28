<script>
  import ContributionGraphManager from "./components/ContributionGraphManager.svelte";
  function getRandomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

function generateRandomContributions() {
  const minCount = 1;
  const maxCount = 20;
  const startDate = new Date('2023-01-01');
  const endDate = new Date('2023-12-31');
  const numContributions = getRandomInt(5, 15);
  
  const contributions = [];

  for (let i = 0; i < numContributions; i++) {
    const randomDate = new Date(startDate.getTime() + Math.random() * (endDate.getTime() - startDate.getTime()));
    const randomCount = getRandomInt(minCount, maxCount);
    contributions.push({ date: randomDate.toISOString().split('T')[0], count: randomCount });
  }

  contributions.sort((a, b) => new Date(a.date) - new Date(b.date));

  return contributions;
}

const contributions = generateRandomContributions();
</script>

<main>
  <ContributionGraphManager contributions={contributions}/>
</main>