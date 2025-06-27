<script>
	import QrCode from 'svelte-qrcode';

	let value = $state('');
	let linkValue = $state('');
	let generateQR = $state(false);
	let isTextEmpty = $state(true);

	function generate() {
		generateQR = true;
		if (value != '') {
			isTextEmpty = false;
			linkValue = value.trim();
		} else {
			console.log('Text is empty!');
			isTextEmpty = true;
		}
	}

	function handleKeyDown(event) {
		if (event.key == 'Enter') generate();
	}
</script>

<div id="box">
	<div id="box2">
		<h1 id="title">QR Code Generator</h1>

		<label for="link">Enter link:</label>
		<input type="text" bind:value name="link" onkeydown={handleKeyDown} />
		<button onclick={generate}>Generate</button>

		{#if generateQR}
			{#if isTextEmpty}
				<h1>Enter some text</h1>
			{:else}
				<div>
					<QrCode value={linkValue} />
				</div>
			{/if}
		{/if}
	</div>
</div>

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

	#box {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: 100dvh;
		border: 1px solid blue;
	}
</style>
