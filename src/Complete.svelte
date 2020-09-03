<script>
  export let close;
  export let count;
</script>

<style>
  .complete-wrapper {
    width: 100vw;
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    background-color: #00000040;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .modal {
    background-color: white;
    pointer-events: none;
    width: 600px;
    height: 400px;
    border-radius: 4px;
    display: flex;
  }
  h1 {
    margin: auto;
    text-align: center;
  }
</style>

<div class="complete-wrapper" on:click={close}>
  <div class="modal">
    <h1>{count}회 만에 성공!</h1>
  </div>
</div>
