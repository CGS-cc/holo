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
    <span>1
				<Card
					name="Bulbasaur"
					img="https://dl.dropboxusercontent.com/s/90ef0fqjxahoed3/dauntless.png?raw=1"
					number="TG241"
					supertype="regular"
					subtypes={["Basic"]}
					rarity="Rare Holo"
				/></span>
    <span>2
        <Card
					name="Articuno"
					img="https://dl.dropboxusercontent.com/s/b3bj4mv45u3zbme/dwarfling.png?raw=1"
					number="TG241"
					supertype="regular"
					subtypes={["Basic"]}
					rarity="Rare Holo"
				/>
    </span>
    <span>3
    <Card
					name="Pikachu"
					img="https://dl.dropboxusercontent.com/s/28h0h9pzcbo1qck/equanimous.png?raw=1"
					number="TG241"
					supertype="regular"
					subtypes={["Basic"]}
					rarity="Rare Holo"
				/></span>
        <span>4<Card
					name="Radiant Venusaur"
					img="https://dl.dropboxusercontent.com/s/8vs93s1rpa3a2a2/colossus.png?raw=1"
					number="TG241"
					supertype="regular"
					subtypes={["Basic"]}
					rarity="Rare Holo"
				/></span>
          <span>5
           <Card
					name="Pikachu"
					img="https://dl.dropboxusercontent.com/s/6bm5wseez3nf9ee/peregrination.png?raw=1"
					number="TG241"
					supertype="regular"
					subtypes={["Basic"]}
					rarity="Rare Holo"
				/></span>
  </CardList>
</main>

<div class="back-to-top">
  <a href="#⚓-top">Back to Top</a>
</div>

<style>
  .back-to-top a {
    color: inherit;
    text-decoration: none;
  }
</style>
