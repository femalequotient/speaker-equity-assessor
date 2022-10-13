<script>
	import './_global.css';
	import Footer from './_components/Footer.svelte';
	import ThemeLoader from '../lib/components/ThemeLoader.svelte';
</script>

<svelte:head>
	<title>Speaker Equity Assessor™</title>
</svelte:head>

<ThemeLoader />
<div id="container">
	<slot />
</div>
<Footer privacyPolicyUrl="https://google.com" />
