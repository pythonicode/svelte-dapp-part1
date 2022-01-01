<script context="module">
	
</script>

<script>
	// IMPORT THESE
	import { browser } from '$app/env';
	import { defaultEvmStores, web3, selectedAccount, connected, chainId, chainData } from 'svelte-web3';

	// This will only render client-side if the browser is available.
	if(browser) {
		defaultEvmStores.setBrowserProvider();
	}

	let address;
	let result;

	const query_balance = async () => {
		if($web3.utils.isAddress(address)) result = $web3.utils.fromWei(await $web3.eth.getBalance(address)).toString() + " " + $chainData?.nativeCurrency?.symbol;
		else result = "Not a valid address.";
	}

</script>

<svelte:head>
	<title>Home</title>
</svelte:head>

<section>
	<div class="flex flex-col justify-center items-center">
		<h1 class="font-bold">{$chainData?.name}</h1>
		<p>Native Currency: {$chainData?.nativeCurrency?.name} ({$chainData?.nativeCurrency?.symbol})</p>
	</div>
	<form on:submit|preventDefault={query_balance} class="m-2 p-2">
		<input bind:value={address} type="text"/>
		<button type="submit">Get Balance</button>
		<div bind:textContent={result} contenteditable="true"></div>
	</form>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
