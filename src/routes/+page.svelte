<script lang="ts">
	import Hero from '$lib/components/Hero.svelte';
	import FeatureRow from '$lib/components/FeatureRow.svelte';
	import FeatureCards from "$lib/components/FeatureCards.svelte";

	// Aquí ajustas tus datos reales
  const ARTIST = {
    name: 'Ximena Ingu',
    spotifyArtistUrl: 'https://open.spotify.com/intl-es/artist/4iF5aAIAVZQKagPignOUNO',
    videoUrl: 'https://www.youtube.com/watch?v=DMAV-lVkMOU&list=OLAK5uy_lQ6HU89UFSTNIq3kt1z59PxiVGMUCMrEQ', 
    sideCardImage: '../lib/images/side-card.png'
  };
</script>

<svelte:head>
	<title>Ximena Ingu</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<Hero
  artistName={ARTIST.name}
  headline="Un ecosistema de emociones"
  subtitle="Explora sus canciones, entra en su mundo y siente cada track como una historia."
  spotifyArtistUrl={ARTIST.spotifyArtistUrl}
  videoUrl={ARTIST.videoUrl}
  albumImage={ARTIST.sideCardImage}
/>

<FeatureCards />
</section>


<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

</style>
