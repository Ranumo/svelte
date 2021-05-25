<script>
  let audioFile = new Audio('/images/music.mp3');
  let volume = 50;
  let adjustVolume = () => (audioFile.volume = volume / 100);
  let playing = false;

  function musa() {
    if (audioFile.paused) {
      audioFile.play();
      playing = true;
    } else {
      audioFile.pause();
      playing = false;
    }
  }

  const rewindAudio = () => (audioFile.currentTime -= 10);
  const forwardAudio = () => (audioFile.currentTime += 10);

</script>

<div class="musicPlayer">
  <div>
    <button on:click={rewindAudio}
      ><img src="/images/rewindButton.jpg" alt="play" /></button
    >
    <button on:click={musa}
      >{#if !playing}<img src="/images/playButton.jpg" alt="play" />
      {:else}
        <img src="images/pauseButton.jpg" alt="pause" />
      {/if}</button
    >
    <button on:click={forwardAudio}
      ><img src="/images/fowardButton.jpg" alt="play" /></button
    >
  </div>
  <div>
    <label for="volume-slider">0</label>
    <input
      id="musicRange"
      class="slide"
      type="range"
      min="0"
      max="100"
      step="1"
      name="volume"
      bind:value={volume}
      on:input={adjustVolume}
    />
    <label for="volume-slider">{volume}</label>
  </div>
</div>

<style>
  .musicPlayer {
    background-color: #ccc;
    width: 300px;
    height: 120px;
    border-bottom-left-radius: 20px;
    border-bottom-right-radius: 20px;
    margin: auto;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    flex-direction: column;
  }

  button {
    border: solid 0px black;
    border-top: solid 3px white;
  }

</style>
