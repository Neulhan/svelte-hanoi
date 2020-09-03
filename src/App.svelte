<script>
  import Tower from "./Tower.svelte";
  import Complete from "./Complete.svelte";
  import { drop } from "./sound.js";
  let length = 7;
  let show = false;

  const close = () => {
    show = false;
    data = JSON.parse(JSON.stringify(dataSet));
    count = 0;
  };

  const dataSet = [
    [...Array(length).keys()].map((value) => {
      return { size: value + 1 };
    }),
    [],
    [],
  ];

  let data = JSON.parse(JSON.stringify(dataSet));

  $: if (data[2].length === length) {
    show = true;
  }

  let count = 0;

  const checkRule = (top, move) => {
    if (top === undefined) {
      return true;
    }
    if (top.size > move.size) {
      return true;
    }
    return false;
  };

  const moveBlock = (blockObj, from, to) => {
    const topBlock = data[to][0];
    const action = checkRule(topBlock, blockObj);
    if (from === to) {
      return;
    }
    if (action) {
      // MOVE
      count++;
      data[from] = data[from].filter((item) => item.size != blockObj.size);
      data[to].unshift(blockObj);
      console.log(`${count}회차: (${blockObj.size}) = ${from} => ${to}`);
      drop();
    }
  };
</script>

<style>
  :global(*) {
    -ms-user-select: none;
    -moz-user-select: -moz-none;
    -khtml-user-select: none;
    -webkit-user-select: none;
    user-select: none;
  }
  .page {
    width: 100%;
    padding-top: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .container {
    width: 930px;
    display: flex;
    justify-content: space-between;
  }
</style>

<div class="page">
  <h1>한오이탑 {count}</h1>
  <div class="container">
    {#each data as tower, i}
      <Tower key={i} {tower} {moveBlock} />
    {/each}
  </div>
</div>
{#if show}
  <Complete {close} {count} />
{/if}
