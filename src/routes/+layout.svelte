<script>
	import './_global.css';
	import Footer from './_components/Footer.svelte';
	import ThemeLoader from '../lib/components/ThemeLoader.svelte';
	import { urls } from '$lib/theme';
</script>

<svelte:head>
	<title>Speaker Equity Assessor™</title>
</svelte:head>

<ThemeLoader />

<div id="siteWrapper">
	<div id="primaryContent">
		<slot />
	</div>
	<div id="footer">
		<Footer privacyPolicyUrl={urls.privacyPolicyUrl} />
	</div>
</div>

<style>
	#siteWrapper {
		display: flex;
		min-height: 100vh;
		flex-direction: column;
	}
	#primaryContent {
		flex: 1;
		display: flex;
		flex-direction: column;
		margin: auto;
		max-width: 45rem;
		align-items: center;
		padding: 10px;
	}
</style>
