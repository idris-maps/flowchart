<script>
  import Split from './components/Split.svelte'
  import Graph from './components/Graph.svelte'

  let value = 'A[Alice] -> B[Bob]\nC[Cecile] --> A\nB .. C'
  let landscape = true

  const onViewChange = d => { landscape = d }
</script>

<Split separatorWidth="5px" {onViewChange}>
  <div slot="left" class:left={landscape} class:top={!landscape}>
    <textarea bind:value={value} />
  </div>
  <div slot="right" class:right={landscape} class:bottom={!landscape}>
    <Graph value={value} />
  </div>
</Split>

<style>
  .left, .right, .top, .bottom {
    width: 100%;
    height: 100%;
  }
  .left, .right {
    overflow-x: hidden;
  }
  .left {
    overflow-y: hidden;
  }
  .top, .bottom {
    overflow-y: hidden;
  }
  .top {
    overflow-x: hidden;
  }
  .right, .bottom {
    background-color: white;
    color: var(--bg-color);
  }
</style>