<script>
  export let closeModal
</script>
<div id="modal" class="modal">
  <div class="modal__header">
    <div class="modal__header__title">
      <div>Modal title</div>
    </div>
    <div class="buttons">
      <div class="button__close-modal" on:click={closeModal}>x</div>
    </div>
  </div>

  <div class="modal__body">
    <div class="modal__body__content">hola mundo soy un modal</div>
  </div>
  
</div>

<style>
  .modal {
    display: none;
    position: absolute;
    width: 300px;
    height: 300px;
    background-color: royalblue;
    color: white;
    font-weight: bold;
    left: 50%;
    top: 50%;
  }
  .modal__header__title {
    display: flex;
    position: absolute;
    width: 100%;
    justify-content: center;
  }

  .buttons {
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }

  .button__close-modal {
    line-height: 1.1;
    width: 16px;
    color: white;
    font-weight: bold;
    background-color: #c3c3c3;
    border: 1px solid grey;
    border-radius: 2px;
    cursor: pointer;
    z-index: 1;
  }

  .modal__body__content {
    display: flex;
    position: absolute;
    width: 100%;
    height: 100%;
    justify-content: center;
    align-items: center;
  }
</style>