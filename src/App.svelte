<script>
  import Character from './lib/Character.svelte';

  let characters = [
    { name: "Ironclad", disabled: false },
    { name: "Silent", disabled: false },
    { name: "Defect", disabled: false },
    { name: "Watcher", disabled: false },
  ];

  let choice = null;

  $: buttonText = choice ? "Reset" : "Roll the dice!";

  $: choosableChars = characters.filter(it => !it.disabled);

  function click() {
    if (choice) {
      characters.map(it => it.chosen = false);
      choice = null;
    } else {
      if (choosableChars.length === 0) return;
      choice = choosableChars[Math.floor(Math.random() * choosableChars.length)];
      choice.chosen = true;
    }
  }
</script>

<main>
  <h1>Let faith chose your hero...</h1>

  <div class="chars">
    {#each characters as character, index}
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <span class="char" on:click={() => { character.disabled = !character.disabled}}>
        <Character {...character} chosen={!!choice && character.name === choice.name} />
      </span>
    {/each}
  </div>

  <button on:click={click}>{buttonText}</button>

  <div>
    <p>
      Click on a character to include/exclude it from choice.
    </p>

    <p class="disclaimer">
      All assets taken from the official <a href="https://slay-the-spire.fandom.com/wiki/">Slay the Spire Wiki</a>.
    </p>
  </div>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    gap: 4em;
  }

  .char {
    cursor: pointer;
  }

  .disclaimer {
    color: #888;
  }
</style>
