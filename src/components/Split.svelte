<script lang="ts">
  import { onMount } from 'svelte'
  import VerticalSplit from "./VerticalSplit.svelte";
  import HorizontalSplit from "./HorizontalSplit.svelte";

  export let separatorColor: string = 'lightgray'
  export let separatorWidth: string = '2px'
  export let onViewChange: (landscape: boolean) => void

  let landscape = true

  const onResize = () => {
    const isLandscape = document.body.offsetHeight < document.body.offsetWidth
    if (isLandscape !== landscape) {
      landscape = isLandscape
      onViewChange(landscape)
    } 
  }

  onMount(onResize)

</script>

<svelte:window on:resize={onResize} />
{#if landscape}
  <VerticalSplit minWidth={30} {separatorColor} {separatorWidth}>
    <div slot="left" class="fullsize">
      <slot name="left"></slot>
    </div>
    <div slot="right" class="fullsize">
      <slot name="right"></slot>
    </div>
  </VerticalSplit>
{:else}
  <HorizontalSplit minHeight={10} {separatorColor} {separatorWidth}>
    <div slot="left" class="fullsize">
      <slot name="left"></slot>
    </div>
    <div slot="right" class="fullsize">
      <slot name="right"></slot>
    </div>
  </HorizontalSplit>
{/if}

<style>
  .fullsize {
    width: 100%;
    height: 100%;
  }
</style>