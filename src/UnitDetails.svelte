<script>
  export let name;
  export let role;
  export let size;
  export let cost;
  export let id;
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  const del = () => dispatch('del', id);

</script>

<h3>#</h3>
<p>{id}</p>
<h3>Role:</h3>
<p>{role}</p>
<h3>Name:</h3>
<p>{name}</p>
<h3>Size:</h3>
<p>{size}</p>
<h3>Cost:</h3>
<p>{cost} points</p>
<button on:click={del}>X</button>
