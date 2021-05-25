<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  const add = () => dispatch('plus');
  const total = () => dispatch('total');

</script>

<button on:click={add}>Add unit</button>
<button on:click={total}>Total points</button>
<slot />

<style>
  button {
    height: 3em;
    width: 12em;
    margin: 1em;
    background-color: rgb(179, 233, 125);
    border-radius: 30px;
  }

  button:hover {
    background-color: rgb(212, 235, 163);
  }

  button:active {
    height: 2.8em;
    width: 11.8em;
  }

</style>
