<script>
	import { ethers } from 'ethers';
	import Token from '../artifacts/contracts/OxyDjinn.sol/Token.json';

  const address = "0x5fbdb2315678afecb367f032d93f642f64180aa3"; // Enviroment variable
  let amount = 0;
	let name = 'notSet';
	let symbol = 'notSet';


	async function getSigner() {
		// A Web3Provider wraps a standard Web3 provider, which is
		// what MetaMask injects as window.ethereum into each page
		const provider = new ethers.providers.Web3Provider(window.ethereum)
		// MetaMask requires requesting permission to connect users accounts
		await provider.send("eth_requestAccounts", []);
		// The MetaMask plugin also allows signing transactions to
		// send ether and pay to change state within the blockchain.
		// For this, you need the account signer...
		const signer = provider.getSigner()
		console.log('Connected MetaMask!', provider)
	}
// Look up the current block number

</script>

<main>
	<div>
		<button on:click={getSigner}>Connect MetaMask</button>
	</div>
	<h2>
		The name of the token is: <h1>'{name}'</h1> and the symbol is <h1>'{symbol}'</h1>
	</h2>
	<div>
		<input bind:value={amount} placeholder="Set amount of COO to buy">
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>