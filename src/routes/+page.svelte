<script>
	import QrCode from 'svelte-qrcode';

	let value = $state('');
	let linkValue = $derived(value.trim());
</script>

<h1 id="title">QR Code Generator</h1>

<label for="link">Enter link:</label>
<input type="text" bind:value name="link" />

{#if value != ''}
	<div>
		<QrCode value={linkValue} />
	</div>
{/if}

<style>
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	#title {
		text-align: center;
		margin: 1rem;
	}
</style>
