<script lang="ts">
	import metaLogo from '$lib/assets/logos/meta.png';
	import fqLogo from '$lib/assets/logos/femaleQuotient.png';
	export let privacyPolicyUrl: string;
</script>

<div class="footer">
	<div class="links">
		<a href={privacyPolicyUrl} target="_blank">Privacy Policy</a>
	</div>
	<div class="logos">
		<img class="fqLogo" src={fqLogo} alt="The Female Quotient" />
		<img class="metaLogo" src={metaLogo} alt="Meta" />
	</div>
</div>

<style>
	a,
	a:visited,
	a:hover {
		color: var(--body-link-color, #0000ff);
		text-decoration: none;
	}
	.footer {
		padding: 20px 0px;
		width: 100%;
		background: rgba(255, 255, 255, 1);
		display: grid;
		justify-content: center;
		row-gap: 10px;
	}
	.links {
		display: flex;
		justify-content: center;
	}
	.logos {
		display: flex;
		justify-content: center;
		column-gap: 60px;
		align-items: center;
	}
	.logos img {
		max-width: 60px;
		display: block;
	}
	.logos img.metaLogo {
		max-width: 120px;
	}
</style>
