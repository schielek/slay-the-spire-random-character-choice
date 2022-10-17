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

<span class:chosen>
  <img 
    src={assets[name]}
    alt={name}
    class:disabled
    class:chosen
    bind:this={image}
    />
</span>

<style>
  img {
    transition: opacity 0.5s ease, filter 0.2s ease, transform 0.25s ease;
  }
  
  .disabled {
    filter: grayscale();
    opacity: 0.25;
  }

  @keyframes pulse {
    from {
      transform: scale(1.0);
    }
    to {
      transform: scale(1.1);
    }
  }

  img.chosen {
    transform: scale(1.4);
  }

  span.chosen {
    display: inline-block;
    animation-name: pulse;
    animation-duration: 2s;
    animation-timing-function: ease-in-out;
    animation-direction: alternate;
    animation-delay: 0s;
    animation-iteration-count: infinite;
    animation-fill-mode: both;
  }
</style>