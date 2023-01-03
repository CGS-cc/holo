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
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="1"
					supertype="regular"
					subtypes={["Basic"]}
					rarity="Common"
				/></span>
    <span>2
        <Card
					name="Articuno"
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="24"
					supertype="regular"
					subtypes={["Basic"]}
					rarity="Rare Holo"
				/>
    </span>
    <span>3
    <Card
					name="Pikachu"
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="SWSH039"
					supertype="regular"
					subtypes={["Basic"]}
					rarity="Rare Holo Galaxy"
				/></span>
        <span>4<Card
					name="Radiant Venusaur"
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="4"
					supertype="regular"
					subtypes={["Basic"]}
					rarity="Radiant Rare"
				/></span>
          <span>5
           <Card
					name="Pikachu"
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="TG241"
					supertype="regular"
					subtypes={["Basic"]}
					rarity="Rare Holo"
				/> 
          </span>
          <span>6
            <Card
					name="Houndoom V"
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="21"
					supertype="regular"
					subtypes={["Basic", "V"]}
					rarity="Rare Holo V"
				/>
          </span>
          <span>7
            <Card
          name="Mew V"
          img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
          number="250"
          supertype="regular"
          subtypes={["Basic", "V", "Fusion Strike"]}
          rarity="Rare Ultra"
        /></span>
        <span>8
<Card
					name="Flareon V"
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="SWSH179"
					supertype="regular"
					subtypes={["Basic", "V", "Single Strike"]}
					rarity="Rare Ultra"
				/>
        </span>
        <span>9
           <Card
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="29"
					supertype="regular"
					subtypes={["VMAX"]}
					rarity="Rare Holo VMAX"
				/> 
        </span>
        <span>10
        <Card
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="215"
					supertype="regular"
					subtypes={["VMAX", "Single Strike"]}
					rarity="Rare Rainbow Alt"
				/></span>
        <span>11
          <Card

					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="SWSH195"
					supertype="regular"
					subtypes={["VSTAR"]}
					rarity="Rare Holo VSTAR"
				/>
        </span>
        <span>12
          <Card
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="196"
					supertype="Trainer"
					subtypes={["Supporter"]}
					rarity="Rare Ultra"
        />
        </span>
        <span>13
          <Card
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="193"
					supertype="regular"
					subtypes={["VMAX"]}
					rarity="Rare Rainbow"
				/>
        </span>
        <span>14
          <Card
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="213"
					supertype="Trainer"
					subtypes={["Stadium"]}
					rarity="Rare Secret"
				/>
        </span>
        <span>15
          <Card
					img="https://dl.dropboxusercontent.com/s/k7qsv879vf3vv8w/test.png?raw=1"
					number="TG16"
					supertype="regular"
					subtypes={["Basic", "V"]}
					rarity="Rare Holo V"
				/>
        </span>          
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
