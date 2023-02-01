
	
  <div class="card__glare" />

<style>
  
	.card__glare {
		transform: translateZ(1.4px);
		background: radial-gradient(
			farthest-corner circle at var(--mx) var(--my),
			rgba(255, 255, 255, 0.8) 10%,
			rgba(255, 255, 255, 0.65) 20%,
			rgba(0, 0, 0, 0.5) 90%
		);
		mix-blend-mode: overlay;
    opacity: calc(var(--o)*.8);
    filter: brightness(0.8) contrast(1.5);
    background: radial-gradient(
			farthest-corner circle at var(--mx) var(--my),
			rgba(255, 255, 255, 0.8) 10%,
			rgba(255, 255, 255, 0.6) 35%,
			rgba(0, 0, 0, 1) 85%
			);
	}

</style>