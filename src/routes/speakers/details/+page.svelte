<script lang="ts">
	import { goto } from '$app/navigation';
	import {
		whiteWomenCount,
		womenOfColorCount,
		whiteMenCount,
		menOfColorCount,
		whiteNonbinaryPeopleCount,
		nonbinaryPeopleOfColorCount,
		sessionText,
		sessionDate,
		sessionLocation,
		sessionDepartment,
		chartPurpose
	} from '$lib/stores';
	import { LogoVersion } from '$lib/types/LogoVersion';
	import Logo from '$lib/components/Logo.svelte';
	import Button from '$lib/components/Button.svelte';

	let showSpeakerProgramNameError = false;
	let loading = false;

	async function createChart(e: Event) {
		if ($sessionText === '') {
			showSpeakerProgramNameError = true;
		} else if (!loading) {
			loading = true;
			const response = await fetch('/api/chart', {
				method: 'POST',
				body: JSON.stringify({
					whiteWomenCount: $whiteWomenCount,
					womenOfColorCount: $womenOfColorCount,
					whiteMenCount: $whiteMenCount,
					menOfColorCount: $menOfColorCount,
					whiteNonbinaryPeopleCount: $whiteNonbinaryPeopleCount,
					nonbinaryPeopleOfColorCount: $nonbinaryPeopleOfColorCount,
					sessionText: $sessionText,
					sessionDate: $sessionDate,
					sessionLocation: $sessionLocation,
					sessionDepartment: $sessionDepartment,
					chartPurpose: $chartPurpose
				}),
				headers: {
					'content-type': 'application/json'
				}
			});
			const { id } = await response.json();
			goto(`/speakers/chart/${id}`);
		}
	}
</script>

<Logo version={LogoVersion.SUBMARK} />
<div class="instructions">
	<h1>Strengthen Speaker Programs</h1>
	<p class="intro">
		You’ve got this! Tell us more about your program. We are cheering you on as you progress. We
		can't wait to see your speaker lineup and celebrate your successes with you!
	</p>
</div>
<form>
	{#if showSpeakerProgramNameError}
		<div class="error">Please provide the name of your speaker program.</div>
	{/if}
	<div class="formItem">
		<label for="sessionText">Name (of speaker program):</label>
		<textarea
			id="sessionText"
			placeholder="e.g. ABC Conference or Top 100 Books XYZ Magazine"
			bind:value={$sessionText} />
	</div>
	<div class="formItem">
		<label for="sessionDate">Date:</label>
		<input type="date" id="sessionDate" bind:value={$sessionDate} />
	</div>
	<div class="formItem">
		<label for="sessionLocation">Location:</label>
		<input
			id="sessionLocation"
			placeholder="e.g. Philadelphia Convention Center"
			bind:value={$sessionLocation} />
	</div>
	<div class="formItem">
		<label for="sessionDepartment">Department:</label>
		<input id="sessionDepartment" placeholder="e.g. Sales" bind:value={$sessionDepartment} />
	</div>
	<div class="formItem">
		<label for="chartPurpose">What are you using this tool for?</label>
		<select id="chartPurpose" bind:value={$chartPurpose}>
			<option value="none">- Select One -</option>
			<option value="events">Events</option>
			<option value="conferences">Conferences</option>
			<option value="editorial">Editorial</option>
			<option value="other">Other</option>
		</select>
	</div>
	<div id="navigation">
		<Button primaryLabel="Back" href="/speakers" />
		<Button primaryLabel="Submit" on:click={createChart} />
	</div>
</form>

<style>
	#navigation {
		justify-content: space-between;
	}
	form {
		max-width: 30rem;
		min-width: 400px;
	}
	.intro {
		max-width: 40rem;
		margin-bottom: 3rem;
	}
</style>
