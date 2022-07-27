<script>
	import { ethers } from 'ethers';
	import Token from '../artifacts/contracts/OxyDjinn.sol/Token.json';

  const address = "0x5fbdb2315678afecb367f032d93f642f64180aa3"; // Enviroment variable/OxyDjinn token
  let amount = 0;
	let name, symbol;

	const provider = new ethers.providers.JsonRpcProvider(); //Localhost provider/connection to the blockchain(read only)
	let hardhat1 = new ethers.Wallet( "ac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80", provider )
	console.log(hardhat1.address)

	async function providerFunctions () {
		console.log(await provider.getBlockNumber())
	}
	providerFunctions()

	// Fetch token contract from the blockchain.
	async function getContract() {
		const oxyDjinn = new ethers.Contract(address, Token.abi, provider)
		name = await oxyDjinn.name()
		symbol = await oxyDjinn.symbol()
		let balance = await oxyDjinn.balanceOf("0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266")
		console.log(balance.toString())
	}
	getContract()

	async function sendTokens() {
		// The COO Contract is currently connected to the Provider,
		// which is read-only. You need to connect to a Signer, so
		// that you can pay to send state-changing transactions.
		const daiWithSigner = contract.connect(signer);

		// Each DAI has 18 decimal places
		const dai = ethers.utils.parseUnits("1.0", 18);

		// Send 1 DAI to "ricmoo.firefly.eth"
		tx = daiWithSigner.transfer("ricmoo.firefly.eth", dai);
	}

	// Request MetaMask provider and fetch the signer.
	async function getSigner() {
		// A Web3Provider wraps a standard Web3 provider, which is
		// what MetaMask injects as window.ethereum into each page
		let provider = new ethers.providers.Web3Provider(window.ethereum)
		// MetaMask requires requesting permission to connect users accounts
		await provider.send("eth_requestAccounts", []);
		// The MetaMask plugin also allows signing transactions to
		// send ether and pay to change state within the blockchain.
		// For this, you need the account signer...
		let signer = provider.getSigner()
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