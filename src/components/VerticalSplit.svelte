<script lang="ts">
  export let separatorColor: string = 'lightgray'
  export let separatorWidth: string = '2px'
  export let minWidth: number = 0

  let mouseX = 0
  let parentLeft = 0
  let parentWidth = 0
  let dragging = false
  let x = 50

  $: parentX = mouseX - parentLeft
  $: _x = Math.max(Math.min(parentX / parentWidth * 100, 100 - minWidth), minWidth)
  $: { if (dragging) { x = _x } }
  $: cols = `calc(${x}% - 1px) ${separatorWidth} calc(${100 - x}% - 1px)`

  const onMouseDown = e => {
    dragging = true
    parentWidth = e.target.parentNode.offsetWidth
    parentLeft = e.target.parentNode.offsetLeft
  }
  const onMouseUp = () => { dragging = false }
  const onMouseMove = e => { mouseX = e.clientX }
</script>

<svelte:window on:mousemove={onMouseMove} on:mouseup={onMouseUp} />
<div class="container" style={`grid-template-columns:${cols}`}>
  <div class:unselectable={dragging}>
    <slot name="left"></slot>
  </div>
  <div
    class="separator"
    on:mousedown={onMouseDown}
    style={`background-color:${separatorColor}`}
  ></div>
  <div class:unselectable={dragging}>
    <slot name="right"></slot>
  </div>
</div>

<style>
  .container {
    display: grid;
    height: 100%;
    width: 100%;
  }
  .separator {
    cursor: col-resize;
  }
  .unselectable {
   -moz-user-select: -moz-none;
   -khtml-user-select: none;
   -webkit-user-select: none;
   -ms-user-select: none;
   user-select: none;
}
</style>
