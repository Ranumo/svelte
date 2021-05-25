<script>
  import UnitDetails from './UnitDetails.svelte';
  export let armylist;
  import { scale } from 'svelte/transition';

</script>

{#each armylist as unit}
  <div class="unitbox" transition:scale>
    <UnitDetails {...unit} on:del />
  </div>
{:else}
  <p>You can start building your army now!</p>
{/each}

<style>
  p {
    color: #dadada;
  }
  .unitbox {
    margin: 10px;
    height: 100px;
    width: 800px;
    margin-left: 30px;
    margin-bottom: 30px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.6);
    -moz-box-shadow: 0 0 10px rgba(0, 0, 0, 0.6);
    -webkit-box-shadow: 0 0 10px rgba(0, 0, 0, 0.6);
    -o-box-shadow: 0 0 10px rgba(0, 0, 0, 0.6);
    background-color: rgb(179, 233, 125);
    display: flex;
    justify-content: center;
    align-items: center;
    justify-content: space-around;
  }

</style>
