<script>
  import Split from './components/Split.svelte'
  import Graph from './components/Graph.svelte'

  let value = 'A[Alice] -> B[Bob]\nC[Cecile] --> A\nB .. C'
</script>

<Split minWidth={30} separatorWidth="5px">
  <div slot="left" class="left">
    <textarea bind:value={value} />
  </div>
  <div slot="right" class="right">
    <Graph value={value} />
  </div>
</Split>

<style>
  .left, .right {
    width: 100%;
    height: 100%;
    overflow-x: hidden;
  }
  .left {
    overflow-y: hidden;
  }
  .right {
    background-color: white;
    color: var(--bg-color);
  }
</style>