<script>
  export let operador = '';
  export let cantidad = 0;
  export let fn = () => {};
</script>

<button  
  disabled={operador === '-' && cantidad === 0 || operador === '+' && cantidad === 20000}
  type='button'
  class='btn btn-primary'
  on:click={fn}
>
  {#if operador == '+'}
    <i class="bi bi-plus"></i>
  {:else}
    <i class="bi bi-dash"></i>
  {/if}
</button>
