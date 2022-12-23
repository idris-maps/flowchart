<script lang="ts">
  export let separatorColor: string = 'lightgray'
  export let separatorWidth: string = '2px'
  export let minHeight: number = 0

  let mouseY = 0
  let parentTop = 0
  let parentHeight = 0
  let dragging = false
  let y = 50

  $: parentY = mouseY - parentTop
  $: _y = Math.max(Math.min(parentY / parentHeight * 100, 100 - minHeight), minHeight)
  $: { if (dragging) { y = _y } }
  $: cols = `calc(${y}% - 1px) ${separatorWidth} calc(${100 - y}% - 1px)`

  const onMouseDown = e => {
    dragging = true
    parentHeight = e.target.parentNode.offsetHeight
    parentTop = e.target.parentNode.offsetTop
  }
  const onMouseUp = () => { dragging = false }
  const onMouseMove = e => { mouseY = e.clientY }
</script>

<svelte:window on:mousemove={onMouseMove} on:mouseup={onMouseUp} />
<div class="container" style={`grid-template-rows:${cols}`}>
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
    cursor:row-resize;
  }
  .unselectable {
   -moz-user-select: -moz-none;
   -khtml-user-select: none;
   -webkit-user-select: none;
   -ms-user-select: none;
   user-select: none;
}
</style>
