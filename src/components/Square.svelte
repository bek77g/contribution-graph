<script>
  export let date;
  export let count;
  export let color;

  const formatDate = (inputDate) => {
    return new Date(inputDate).toLocaleDateString(undefined, { month: 'short', day: 'numeric', weekday: 'long' });
  };
</script>

<style>
    .square {
        position: relative;
        background-color: #ebedf0;
    }
    .square:hover .tooltip {
        top: -40px;
        opacity: 1;
        visibility: visible;
        pointer-events: auto;
    }
    .tooltip {
        position: absolute;
        top: 0;
        left: 50%;
        transform: translateX(-50%);
        white-space: nowrap;
        font-size: 12px;
        background: #ffffff;
        color: #000;
        padding: 5px 8px;
        border-radius: 5px;
        box-shadow: 0 10px 10px rgba(0, 0, 0, 0.1);
        opacity: 0;
        pointer-events: none;
        transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        z-index: 100;
    }
    .tooltip::before {
        position: absolute;
        content: "";
        height: 8px;
        width: 8px;
        background: #ffffff;
        bottom: -3px;
        left: 50%;
        transform: translate(-50%) rotate(45deg);
        transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
    }
</style>

<li class="square" style="background-color: {color}">
  {#if count > 0}
    <p class="tooltip">
      {formatDate(date)}: {count} {count === 1 ? 'contribution' : 'contributions'}
    </p>
  {/if}
</li>
