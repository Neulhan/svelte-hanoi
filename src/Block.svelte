<script>
  export let block;
  export let isTop;
  export let moveBlock;
  export let from;
  let hold;
  let to;

  let bound;

  let blockElement;

  const pointerMoveListener = (e) => {
    const towerNow = e.target.closest(".tower");
    bound = {
      top: e.clientY,
      left: e.clientX,
    };
    if (towerNow != null) {
      to = towerNow.getAttribute("key");

      return;
    }
    to = from;
  };
  const pointerUpListener = (e) => {
    moveBlock(block, from, to);
    hold = false;
    bound = undefined;
    window.removeEventListener("pointermove", pointerMoveListener);
    window.removeEventListener("pointerup", pointerUpListener);
  };

  const pointerListener = (e) => {
    // console.log(e);
    if (!isTop) {
      return;
    }
    if (e.type === "pointerdown") {
      hold = true;
      bound = e.target.getBoundingClientRect();
      window.addEventListener("pointermove", pointerMoveListener);
      window.addEventListener("pointerup", pointerUpListener);
    }
  };
</script>

<style>
  .block {
    text-align: center;
    background-color: #888;
    color: white;
    margin-top: 2px;
    height: 30px;
    line-height: 30px;
    cursor: pointer;
  }
  .hold {
    opacity: 0.2;
    pointer-events: none;
    border: 1px dashed #888888;
  }
</style>

<div
  bind:this={blockElement}
  key={block.size}
  on:pointerdown={pointerListener}
  on:pointerup={pointerListener}
  onselectstart="return false"
  class="block"
  class:hold
  style="width: {block.size * 40}px; {bound ? `position:absolute; top:${bound.top - 15}px; left:${bound.left - 30}px` : ''}">
  {block.size}
</div>
