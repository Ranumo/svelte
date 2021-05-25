<script>
  import Modal from './Modal.svelte';
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  const cancel = () => dispatch('cancel');
  const submit = () => dispatch('submit');

  export let role;
  export let name;
  export let size;
  export let cost;

</script>

<Modal>
  <div slot="header">
    <h2>Add unit</h2>
    <p>Give details for your unit</p>
  </div>
  <div>
    <p>Role:</p>
    <input type="text" bind:value={role} />
  </div>
  <div>
    <p>Name:</p>
    <input type="text" bind:value={name} />
  </div>
  <div>
    <p>Size:</p>
    <input type="number" bind:value={size} />
  </div>
  <div>
    <p>cost:</p>
    <input type="number" bind:value={cost} />
  </div>
  <div slot="footer">
    <button on:click={submit}>Submit</button>
    <button on:click={cancel}>Cancel</button>
  </div>
</Modal>

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
