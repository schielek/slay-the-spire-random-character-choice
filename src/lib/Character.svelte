<script>
  import ironclad from '../assets/Ironclad.webp';
  import silent from '../assets/Silent.webp';
  import defect from '../assets/Defect.webp';
  import watcher from '../assets/Watcher.webp';
  import party, { Circle, variation } from "party-js";

  export let name;
  export let disabled;
  export let chosen;

  const assets = {
    "Ironclad": ironclad,
    "Silent": silent,
    "Defect": defect,
    "Watcher": watcher,
  }

  let image;
  $: imageRect = (image == undefined) && !chosen  ? null : image.getBoundingClientRect();
  $: console.log(imageRect)

  $: if(chosen) party.confetti(new Circle((imageRect.left + imageRect.right) / 2, imageRect.top - 0.1 * (imageRect.top - imageRect.bottom), 3), {
    count: 80,
    spread: 30,
    size: variation.skew(1.2, 0.8),
    speed: variation.range(400, 700),
  })
</script>

<img 
  src={assets[name]}
  alt={name}
  class:disabled
  class:chosen
  bind:this={image}
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