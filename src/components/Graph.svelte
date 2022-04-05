<script lang="ts">
	import graph from './graph.js'

	export let value: string = ''
	let div: HTMLDivElement | undefined = undefined
  let svg: string = ''

	$: {
		svg = value.trim() !== '' ? graph(value) : ''	
		if (div) {
			div.innerHTML = svg
		}
	}

  $: href = `data:application/octet-stream,${encodeURIComponent(svg)}`
</script>

<div class="btns">
  <a href="/about.html">
    <button>About</button>
  </a>
  <a {href} download="graph.svg">
    <button>Download</button>
  </a>
</div>
<div bind:this={div} />

<style>
  .btns {
    position: fixed;
    bottom: 0.5em;
    right: 1em;
  }
</style>