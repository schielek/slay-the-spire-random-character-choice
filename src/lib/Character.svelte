<script>
  import ironclad from '../assets/Ironclad.webp';
  import silent from '../assets/Silent.webp';
  import defect from '../assets/Defect.webp';
  import watcher from '../assets/Watcher.webp';

  export let name;
  export let disabled;
  export let chosen;

  const assets = {
    "Ironclad": ironclad,
    "Silent": silent,
    "Defect": defect,
    "Watcher": watcher,
  }
</script>

<img 
  src={assets[name]}
  alt={name}
  class:disabled
  class:chosen
  />

<style>
  img {
    transition: opacity 0.5s ease, filter 0.2s ease, transform 0.25s ease;
  }
  
  .disabled {
    filter: grayscale();
    opacity: 0.25;
  }

  .chosen {
    transform: scale(1.5);
  }
</style>