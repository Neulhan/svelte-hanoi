<script>
  import Block from "./Block.svelte";
  export let tower;
  export let key;
  export let moveBlock;
</script>

<style>
  .tower {
    width: 300px;
    height: 600px;
    border: 1px solid #ccc;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-end;
  }
</style>

<div class="tower" {key}>
  {#each tower as block, i}
    <Block from={key} {block} {moveBlock} isTop={i === 0 ? true : false} />
  {/each}
</div>
