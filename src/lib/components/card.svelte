<script>
  import { spring } from "svelte/motion";
  import { clamp, round } from "../helpers/Math.js";

  import Glare from "../components/card-glare.svelte";
  import Shine from "../components/card-shine.svelte";

  export let back_img =
    "https://dl.dropboxusercontent.com/s/8vg2bgkhiyu2fcu/background.png?raw=1";
  export let img = "";

  export let name = "";
  export let number = "0";
  export let subtypes = "basic";
  export let supertype = "regular";
  export let rarity = "common";
  export let gallery = false;

  let thisCard;
  let rotator;
  let active = false;
  let interacting = false;
  let loading = true;

  const springR = { stiffness: 0.066, damping: 0.25 };
  const springD = { stiffness: 0.033, damping: 0.45 };
  let springRotate = spring({ x: 0, y: 0 }, springR);
  let springGlare = spring({ x: 50, y: 50, o: 0 }, springR);
  let springBackground = spring({ x: 50, y: 50 }, springR);
  let springRotateDelta = spring({ x: 0, y: 0 }, springD);
  let springTranslate = spring({ x: 0, y: 0 }, springD);
  let springScale = spring(1, springD);


  const interact = (e) => {


    interacting = true;

    if (e.type === "touchmove") {
      e.clientX = e.touches[0].clientX;
      e.clientY = e.touches[0].clientY;
    }

    const $el = e.target;
    const rect = $el.getBoundingClientRect(); // get element's current size/position
    const absolute = {
      x: e.clientX - rect.left, // get mouse position from left
      y: e.clientY - rect.top, // get mouse position from right
    };
    const percent = {
      x: round((100 / rect.width) * absolute.x),
      y: round((100 / rect.height) * absolute.y),
    };
    const center = {
      x: percent.x - 50,
      y: percent.y - 50,
    };

    springBackground.stiffness = springR.stiffness;
    springBackground.damping = springR.damping;
    springBackground.set({
      x: round(50 + percent.x / 4 - 12.5),
      y: round(50 + percent.y / 3 - 16.67),
    });
    springRotate.stiffness = springR.stiffness;
    springRotate.damping = springR.damping;
    springRotate.set({
      x: round(-(center.x / 3.5)),
      y: round(center.y / 2),
    });
    springGlare.stiffness = springR.stiffness;
    springGlare.damping = springR.damping;
    springGlare.set({
      x: percent.x,
      y: percent.y,
      o: 1,
    });
  };

  const interactEnd = (e, delay = 500) => {
    setTimeout(function () {
      const snapStiff = 0.01;
      const snapDamp = 0.06;
      interacting = false;

      springRotate.stiffness = snapStiff;
      springRotate.damping = snapDamp;
      springRotate.set({ x: 0, y: 0 }, { soft: 1 });

      springGlare.stiffness = snapStiff;
      springGlare.damping = snapDamp;
      springGlare.set({ x: 50, y: 50, o: 0 }, { soft: 1 });

      springBackground.stiffness = snapStiff;
      springBackground.damping = snapDamp;
      springBackground.set({ x: 50, y: 50 }, { soft: 1 });
    }, delay);
  };

  const deactivate = (e) => {
    interactEnd();
  };

  $: styles = `
		--mx: ${$springGlare.x}%;
		--my: ${$springGlare.y}%;
		--tx: ${$springTranslate.x}px;
		--ty: ${$springTranslate.y}px;
		--s: ${$springScale};
		--o: ${$springGlare.o};
		--rx: ${$springRotate.x + $springRotateDelta.x}deg;
		--ry: ${$springRotate.y + $springRotateDelta.y}deg;
		--pos: ${$springBackground.x}% ${$springBackground.y}%;
		--posx: ${$springBackground.x}%;
		--posy: ${$springBackground.y}%;
		--hyp: ${
      clamp( Math.sqrt(
        ($springGlare.y - 50) * ($springGlare.y - 50) +
          ($springGlare.x - 50) * ($springGlare.x - 50)
      ) / 50, 0, 1)
    };
	`;

  $: {
    rarity = rarity.toLowerCase();
    number = number.toLowerCase();
    gallery = number.startsWith("tg");

  }

  const imageLoader = (e) => {
    loading = false;
  };


</script>


<div
  class="card"
  class:active
  class:interacting
  class:loading
  data-number={number}
  data-subtypes={subtypes}
  data-supertype={supertype}
  data-rarity={rarity}
  data-gallery={gallery}
  style={styles}
  bind:this={thisCard}
>
  <div class="card__translater">
    <button
      class="card__rotator"
      bind:this={rotator}
      on:pointermove={interact}
      on:mouseout={interactEnd}
      on:blur={deactivate}
      aria-label="Expand theCard; {name}."
      tabindex="0"
    >
      <img
        class="card__back"
        src={back_img}
        alt=""
        loading="lazy"
      />
      <div class="card__front">
        <img
          src={img}
          alt=""
          on:load={imageLoader}
          loading="lazy"
        />
        <Shine {subtypes} {supertype} />
        <Glare {subtypes} {rarity} />
      </div>
    </button>
  </div>
</div>

<style>
  :root {
    --mx: 50%;
    --my: 50%;
    --s: 1;
    --o: 0;
    --tx: 0px;
    --ty: 0px;
    --rx: 0deg;
    --ry: 0deg;
    --pos: 50% 50%;
    --posx: 50%;
    --posy: 50%;
    --hyp: 0;
  }

  .card {
    display: grid;
		grid-template-columns: 3fr;
		grid-gap: 2vw;
		transform-style: preserve-3d;
		height: 100%;
		max-width: 350px;
		margin: auto;
		padding: 50px;
		position: relative;
    --radius: 4.55%;
    --back: #004177;
    --glow: #69d1e9;
    z-index: calc(var(--s) * 100);
    transform: translate3d(0, 0, 0.1px);
    -webkit-transform: translate3d(0, 0, 0.1px);
    will-change: transform, visibility;
    transform-style: preserve-3d;
    -webkit-transform-style: preserve-3d;
  }

  .card.interacting {
    z-index: calc(var(--s) * 120);
  }

  .card.active .card__translater,
  .card.active .card__rotator {
    touch-action: none;
  }

  .card__translater,
  .card__rotator {
    display: grid;
    perspective: 600px;
    transform-origin: center;
    -webkit-transform-origin: center;
    will-change: transform;
  }

  .card__translater {
    width: auto;
    position: relative;
    transform: translate3d(var(--tx), var(--ty), 0) scale(var(--s));
    -webkit-transform: translate3d(var(--tx), var(--ty), 0) scale(var(--s));
  }

  .card__rotator {
    transform: rotateY(var(--rx)) rotateX(var(--ry));
    transform-style: preserve-3d;
    -webkit-transform: rotateY(var(--rx)) rotateX(var(--ry));
    -webkit-transform-style: preserve-3d;
    box-shadow: 0px 10px 20px -5px black;
    border-radius: var(--radius);
    outline: none;
    transition: box-shadow 0.4s ease, outline 0.2s ease;
  }
  button.card__rotator {
    appearance: none;
    -webkit-appearance: none;
    border: none;
    background: top;
    padding: 0;
  }

  .card.active .card__rotator {
    box-shadow: 0 0 10px 0px var(--glow), 0 0 10px 0px var(--glow),
      0 0 30px 0px var(--glow);
  }

  .card__rotator:focus {
    box-shadow: 0 0 10px 0px var(--glow), 0 0 10px 0px var(--glow),
      0 0 30px 0px var(--glow);
  }

  .card.active .card__rotator:focus {
    box-shadow: 0px 10px 30px 3px black;
  }

  .card__rotator :global(*) {
    width: 100%;
    display: grid;
    grid-area: 1/1;
    border-radius: var(--radius);
    image-rendering: optimizeQuality;
    transform-style: preserve-3d;
    -webkit-transform-style: preserve-3d;
  }

  .card__rotator img {
    outline: 1px solid transparent;
    aspect-ratio: 0.716;
    height: auto;
  }

  .card__back {
    background-color: var(--back);
    transform: rotateY(180deg) translateZ(1px);
    -webkit-transform: rotateY(180deg) translateZ(1px);
    backface-visibility: visible;
  }

  .card__front,
  .card__front * {
    backface-visibility: hidden;
  }

  .card__front {
    opacity: 1;
    transition: opacity 0.33s ease-out;
  }

  .loading .card__front {
    opacity: 0;
  }

  .loading .card__back {
    transform: rotateY(0deg);
    -webkit-transform: rotateY(0deg);
  }
</style>
