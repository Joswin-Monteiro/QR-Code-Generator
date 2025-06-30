<script>
	import QrCode from 'svelte-qrcode';
	import { innerWidth } from 'svelte/reactivity/window';

	let value = $state('');
	let linkValue = $state('');
	let size = $state(0);
	let isPreview = $state(true);

	if (innerWidth.current < 500) {
		size = 250;
	} else {
		size = 400;
	}

	function generate() {
		linkValue = value.trim();
		if (linkValue == '') {
			isPreview = true;
		} else {
			isPreview = false;
		}
		if (innerWidth.current < 500) {
			size = 250;
		} else {
			size = 400;
		}
	}

	function handleKeyDown(event) {
		if (event.key == 'Enter') generate();
	}

	function focus(node) {
		node.focus();
	}

	$effect(() => {
		if (value) value.focus({ focusVisible: true });
	});
</script>

<div id="box">
	<div id="box2">
		<h1 id="title">QR Code Generator</h1>

		<div class="container">
			<label for="link">Enter text:</label>
			<input
				type="text"
				bind:value
				name="link"
				onkeydown={handleKeyDown}
				placeholder="Ex: https://www.example.com"
				use:focus
			/>
			<button onclick={generate}>Generate</button>
		</div>

		<div class="container" id="container2" style:height={`${size}px;`}>
			{#if isPreview}
				<QrCode value="https://www.example.com" {size} color="#d1d1d1" />
			{:else}
				<QrCode value={linkValue} {size} />
			{/if}
		</div>
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
	}

	.container {
		text-align: center;
	}

	#container2 {
		margin: 10px;
		display: flex;
		align-items: center;
		justify-content: center;
		text-align: center;
		padding: 2rem;
	}
</style>
