<script>
	import CardList from "./cards.svelte";
	import Card from "./lib/components/card.svelte";
  import { onMount } from "svelte";

	onMount(() => {
		const $headings = document.querySelectorAll("h1,h2,h3");
		const $anchor = [...$headings].filter((el) => {
			const id = el.getAttribute("id")?.replace(/^.*?-/g,"");
			const hash = window.location.hash?.replace(/^.*?-/g,"")
			return id === hash;
		})[0];
		if( $anchor ) {
			setTimeout(() => {
				$anchor.scrollIntoView();
			},100);
		}
	});
</script>

<main>
	<CardList>
				<Card
					name="Bulbasaur"
					img="https://dl.dropboxusercontent.com/s/90ef0fqjxahoed3/dauntless.png?raw=1"
					number="TG241"
					supertype="regular"
					subtypes="basic"
					rarity="Rare Holo"
				/>
  </CardList>
</main>
