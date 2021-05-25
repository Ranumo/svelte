<script>
  import user from './loginStore.js';
  import Armybuilder from './Armybuilder.svelte';
  import Choose from './Choose.svelte';
  import AddWindow from './AddWindow.svelte';
  import MusicPlayer from './MusicPlayer.svelte';
  import { tweened } from 'svelte/motion';
  import { slide } from 'svelte/transition';
  import Icon from 'fa-svelte';
  import { faCircle } from '@fortawesome/free-solid-svg-icons/faCircle';

  let icon = faCircle;
  let armylist = [];
  let armyPoints = [];

  let showAddWindow = false;

  const nimiTween = tweened(0, {
    duration: 1000,
  });

  const startTween = () => {
    nimiTween.set(1);
  };

  const passTween = tweened(0, {
    delay: 1000,
    duration: 1000,
  });

  const startAlsoTween = () => {
    passTween.set(1);
  };

  const endTween = () => {
    passTween.set(0);
    nimiTween.set(0);
  };

  let inputUser;
  let inputPass;
  let activeCommandPanel = false;

  const clear = () => {
    inputUser = '';
    inputPass = '';
  };

  function login() {
    if (inputUser === $user.ktun) {
      if (inputPass === $user.salasana) {
        activeCommandPanel = true;
        clear();
        startTween();
        startAlsoTween();
      } else {
        clear();
      }
    } else {
      clear();
    }
  }

  function logout() {
    activeCommandPanel = false;
    endTween();
  }

  let role = '';
  let name = '';
  let size = '';
  let cost = '';
  $: unitCost = size * cost;
  $: idNumberGenerator = armylist.length + 1;

  $: choiseUnit = {
    role: role,
    name: name,
    size: size,
    cost: unitCost,
    id: idNumberGenerator,
  };

  function clearChoiseUnit() {
    role = '';
    name = '';
    size = '';
    cost = '';
  }

  function addUnit() {
    showAddWindow = true;
  }

  function cancelAddUnit() {
    showAddWindow = false;
    clearChoiseUnit();
  }

  function submitAddUnit() {
    armyPoints.push(choiseUnit.cost);
    armyPoints = armyPoints;
    armylist.push(choiseUnit);
    armylist = armylist;
    clearChoiseUnit();
    showAddWindow = false;
  }

  const removeId = (ce) => {
    console.log(ce.detail);
    armylist = armylist.filter((x) => x.id !== ce.detail);
  };

  $: totalPoints = 0;

  const pointCalculator = () => {
    totalPoints = 0;
    for (let i = 0; i <= armylist.length - 1; i++) {
      totalPoints += armylist[i].cost;
      totalPoints = totalPoints;
    }
    return totalPoints;
  };

</script>

<main>
  <div class="banner">
    {#if !activeCommandPanel}
      <h3>Please log into your account to use the application</h3>
    {:else}
      <h3>Logged in as {$user.ktun}</h3>
    {/if}
  </div>
  <div class="login">
    <div>
      <progress value={$nimiTween} />
    </div>

    <div>
      <p>Username:</p>
      <input type="text" bind:value={inputUser} />
    </div>
    <div>
      <p>Password:</p>
      <input type="text" bind:value={inputPass} />
    </div>
    {#if !activeCommandPanel}
      <button on:click={login}>Login</button>
    {:else}
      <button on:click={logout}>Logout</button>
    {/if}
    <div>
      <progress value={$passTween} />
    </div>
  </div>
  {#if activeCommandPanel}
    <div
      class="content"
      in:slide={{ delay: 2000, duration: 2000, x: 0, y: 3000 }}
      out:slide={{ delay: 2000, duration: 2000 }}
    >
      <Choose on:plus={addUnit} on:total={pointCalculator}>
        <h3>{totalPoints} / 2000 Points</h3>
      </Choose>
      <Armybuilder {armylist} on:del={removeId} />
    </div>
  {/if}
  {#if showAddWindow}
    <AddWindow
      bind:role
      bind:name
      bind:size
      bind:cost
      on:submit={submitAddUnit}
      on:cancel={cancelAddUnit}
    />
  {/if}

  <MusicPlayer />
  <Icon {icon} />
  <i class="fas fa-play" />
</main>

<style>
  .banner {
    background-image: url('/images/bannerNecron.jpg');
    background-repeat: no-repeat;
    background-size: 100% auto;
    height: 500px;
    display: flex;
    justify-content: center;
    align-items: flex-end;
    border-top-left-radius: 20px;
    border-top-right-radius: 20px;
  }

  .login {
    background-color: #131812;
    border-bottom-left-radius: 20px;
    border-bottom-right-radius: 20px;
    gap: 1em;
    padding: 0.5em;
    padding-bottom: 1em;
    display: flex;
    justify-content: center;
    justify-content: space-evenly;
    align-items: flex-end;
  }

  .login p {
    color: rgb(255, 255, 255);
  }

  .login button {
    height: 2em;
    align-items: flex-end;
    width: 5em;
    background-color: rgba(179, 255, 104, 0.664);
  }

  .login input {
    background-color: rgba(179, 255, 104, 0.664);
  }

  .login button:hover {
    height: 2.1em;
    width: 5.1em;
  }

  .login input:focus {
    background-color: rgba(238, 255, 0, 0.664);
  }

  .login button:active {
    background-color: rgba(238, 255, 0, 0.664);
  }
  main {
    text-align: center;
    padding: 1em;
    min-width: 860px;
    max-width: 860px;
    margin: 0 auto;
    font-family: Arial, Helvetica, sans-serif;
  }

  h3 {
    color: #fff;
    font-size: 1.5em;
  }
  progress {
    background-color: rgba(238, 255, 0, 0.664);
    border-radius: 10px;
  }

  .content {
    width: 860px;

    background-color: rgb(78, 78, 78);
    border-radius: 20px;
    border: solid 1px black;
  }

</style>
